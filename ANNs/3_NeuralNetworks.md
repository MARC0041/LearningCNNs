# Steps
1. Prepare data loaders
2. Build a network
3. Loop over
    1. forward pass
    2. Calculate loss
    3. Calculate gradients
    4. Change weights based on gradients
    `weights -= weight_gradient * learning_rate`

## Creating the network
```
import torch
import torch.nn
import torch.nn.Functional as F
import torch.optim as optim

# Define the class Net
class Net(nn.Module):
    def __init__(self):    
    	# Define all the parameters of the net
        super(Net, self).__init__()
        self.fc1 = nn.Linear(28 * 28 * 1, 200)
        self.fc2 = nn.Linear(200, 10)

    def forward(self, x):   
    	# Do the forward pass
        x = F.relu(self.fc1(x))
        x = self.fc2(x)
        return x
```
## Training the network
```
# Instantiate the Adam optimizer and Cross-Entropy loss function
model = Net()   
optimizer = optim.Adam(model.parameters(), lr=3e-4)
criterion = nn.CrossEntropyLoss()
  
for batch_idx, data_target in enumerate(train_loader):
    data = data_target[0]
    target = data_target[1]
    data = data.view(-1, 28 * 28)
    optimizer.zero_grad()

    # Complete a forward pass
    output = model(data)

    # Compute the loss, gradients and change the weights
    loss = criterion(output, target)
    loss.backward()
    optimizer.step()
```
---
## Evaluate model

```
# Set the model in eval mode
model.eval()

for i, data in enumerate(test_loader, 0):
    inputs, labels = data
    
    # Put each image into a vector
    inputs = inputs.view(-1, 28*28)
    
    # Do the forward pass and get the predictions
    outputs = model(inputs)
    # Get the maximum along dim=1. returns max_elem, max_ind
    _, outputs = torch.max(outputs.data, 1)
    total += labels.size(0)
    correct += (outputs == labels).sum().item()
print('The testing set accuracy of the network is: %d %%' % (100 * correct / total))
```

### Illustration of torch.max
```
p = torch.randn([2, 3])
# Get the maximum along dim = 0 (axis = 0), dim=0 means the rows
max_elements, max_idxs = torch.max(p, dim=0)
print(p)
print(max_elements)
print(max_idxs)
```
```
tensor([[-0.0665,  2.7976,  0.9753],
        [ 0.0688, -1.0376,  1.4443]])
tensor([0.0688, 2.7976, 1.4443])
tensor([1, 0, 1])
```