# Softmax
The following us the equation for softmax

$
\sigma(z)_j=\frac{e^{z_j}}{\sum_{k=1}^k e^{z_k}} \text { for } j=1, \ldots, k
$

if z = [10.2, 5.1, -1.7], then
$z_1 = e^{10.2} / (e^{10.2} +e^{5.1} +e^{-1.7} )$
# CrossEntropyLoss
If the final layer gave you predictions of [10.2, 5.1, -1.7]

softmax = 
    [\
        $e^{10.2} / (e^{10.2} +e^{5.1} +e^{-1.7} ), \\
        e^{5.1} / (e^{10.2} +e^{5.1} +e^{-1.7} ),\\
        e^{-1.7} / (e^{10.2} +e^{5.1} +e^{-1.7} )
        \\
        $]

And we know that: 

$L_{\text {cross-entropy }}(\hat{\mathbf{y}}, \mathbf{y})=-\sum y_i \log \left(\hat{y}_i\right)$

Therefore, if the target is [1,0,0], then
```
    loss = - (
        1 * log(0.99393349019) + 
        0 * log(0.00605976059) + 
        0 * log(0.00000674921))
```


# Pytorch code
```
logits = torch.tensor([[10.2, 5.1, -1.7]])
ground_truth = torch.tensor([0]) # this kind of means the target
criterion = nn.CrossEntropyLoss()

loss = criterion(logits, ground_truth)
print(f"loss: {loss}")
```

Note that the `ground_truth` variable is the multiclass scalar value. and may not be an array. 