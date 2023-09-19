# LearningDeepLearning

## Concepts Learnt
- Transfer Learning
    - We can use pre-trained weights in resnet18 for example
    - when do we do this? If we do 


___
## Open Questions
### Other Deep learning questions:
1. When to use each loss function? e.g. RMSE vs logistics loss
2. When to use each optimizer? e.g. Adam optimizer
3. 
### Unfamiliar Syntax used in CNN:
- what is unsqueeze? ` img = torch.tensor(img).unsqueeze(0)`
- `pred.cpu()`
- what is `batch` in `def validation_step(self, batch, batch_idx):`
- How to use `TensorBoard`
- why use the shape (1,) in `random_seed = torch.randint(0, 1000000, (1,)).item()` and what is `.item()`?
- Why img object was created and overwritten 2x? explain `torchvision.make_grid`?  How exactly the tensorboard logs these info?
    ```
    def log_images(self, x_ray, pred, label, name):
    results = []
    std = 0.252
    mean = 0.494
    # Here we create a grid consisting of 4 predictions
    for i in range(4):
        coords_labels = label[i]
        coords_pred = pred[i]
        img = ((x_ray[i] * std)+mean).numpy()[0]
        
        # Extract the coordinates from the label
        ...
        img = cv2.rectangle(img, (x0, y0), (x1, y1), (0, 0, 0), 2)
        
        # Extract the coordinates from the prediction           
        ...
        img = cv2.rectangle(img, (x0, y0), (x1, y1), (1, 1, 1), 2)
        
        
        results.append(torch.tensor(img).unsqueeze(0))
    grid = torchvision.utils.make_grid(results, 2)
    self.logger.experiment.add_image(f"{name} Prediction vs Label", grid, self.global_step)
        ```
- what is `configure_optimizers` in the model?
- what is `self.optimizer` in `configure_optimizers` method?
- Where to save and how to use `ckpt` files?
- what additional steps are needed because gpu/cuda is unavailable for mac / how to use mps (multi-processing / metal) in mac
- what is `device = torch.device(...)`, and `model = model.load_from_checkpoint("weight.ckpt") ` , `model.eval()`,and `model.to(device)`
- what is stack in `preds=torch.stack(preds)`
### Unfamiliar concepts in CNNs:
1. CNNs explanation can be found here: 
2. Here is a good video explaining class activation maps:
https://www.youtube.com/watch?v=vTY58-51XZA and 
https://www.pinecone.io/learn/class-activation-maps/ 
3. How to go from X inputs to Y outputs in a Convolutional layer:
https://www.youtube.com/watch?v=KTB_OFoAQcc
    ```
    a. Say I have 5 filters for conv1. 
    b. Therefore I will have 5 images outputted after the conv1. If each output image is of dimensions (Row,Width). 
    c. The stack of images will be of dimensions (numFilters,Row,Width)
    use a volume kernel. 
    d. For 3 images, the kernel would spend a 3d volume (3 x KernalHeight x KernalWidth) and therefore the kernal is 3d instead of 2d. 
    ```
4. How to prevent vanishing and exploding gradients?


