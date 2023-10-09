# Initialize the Network
You are using the MNIST dataset to predict the integer. The input images are 28x28. 
Because of self.pool, each pooling layer halves the size of the image. 
Note that the conv layer keeps the dimensions because padding is 1. (I think default stride is 1)
The last linear layer should probably allow for `nn.Linear(-1, 10)` ?? 
```
class Net(nn.Module):
    def __init__(self):
        super(Net, self).__init__()
        
        # Instantiate two convolutional layers
        self.conv1 = nn.Conv2d(in_channels=1, out_channels=5, kernel_size=3, padding=1)
        self.conv2 = nn.Conv2d(in_channels=5, out_channels=10, kernel_size=3, padding=1)
        
        # Instantiate the ReLU nonlinearity
        self.relu = nn.ReLU()
        
        # Instantiate a max pooling layer
        self.pool = nn.MaxPool2d(kernel_size=2, stride=2)
        
        # Instantiate a fully connected layer
        # as there are 28x28 pixels, if the images are 1/4, the resulting image is 7x7
        self.fc = nn.Linear(10*7*7, 10) 

    def forward(self, x):
        # Apply conv followd by relu, then in next line pool
        x = self.relu(self.conv1(x))
        x = self.pool(x)

        # Apply conv followd by relu, then in next line pool
        x = self.relu(self.conv2(x))
        x = self.pool(x)

        # Prepare the image for the fully connected layer
        x = x.view(-1, 7*7*10)

        # Apply the fully connected layer and return the result
        return self.fc(x)
```