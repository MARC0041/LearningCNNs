# Training CNNs
## Imports
```
import torch
import torchvision
import torchvision.transforms as transforms
import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim
```
## Dataloaders
```
transform = transforms.Compose(
    [
        transforms.ToTensor(),
        transforms.Normalize((0.5,0.5,0.5), (0.5,0.5,0.5))
    ]
)
trainset = torchvision.datasets.CIFAR(root='/date', train=True,
                                    download=True, transform=transform)
trainloader = torchvision.utils.data.DataLoader(trainset, batch_size=128,
                                    shuffle=True, num_workers=2)

                                    
testset = torchvision.datasets.CIFAR(root='/date', train=False,
                                    download=True, transform=transform)
testloader = torchvision.utils.data.DataLoader(trainset, batch_size=128,
                                    shuffle=False, num_workers=2)
```