# Deep Learning with PyTorch for Medical Image Analysis

https://nlbsg.udemy.com/course/deep-learning-with-pytorch-for-medical-image-analysis/learn/lecture/29067076#overview

The following topics are covered:

- NumPy
- Machine Learning Theory
- Test/Train/Validation Data Splits
- Model Evaluation - Regression and Classification Tasks
- Tensors with PyTorch
- Convolutional Neural Networks
- Medical Imaging
- Interpretability of a network's decision - Why does the network do what it does?
- A state of the art high level pytorch library: pytorch-lightning
- Tumor Segmentation
- Three-dimensional data
- and many more

# to begin:
conda create -n pytorch_biomed python=3.8.0 OR conda create --name pytorch_biomed python=3.8.0
<!-- conda create --name pytorch_nightly python=3.8.0 -->
conda activate pytorch_biomed
pip install -r requirements.txt


Remember to add the env:
python -m ipykernel install --user --name=pytorchenv
Change kernel to pytorchenv

# Code is not working: import pytorch_lightning as pl
pip install setuptools==59.5.0
pip install protobuf=3.20.0


# Facing some issue with import pytorch-lightning. AttributeError: module 'distutils' has no attribute 'version'
# try updating pytorch to newer version. currently is 1.9.1
conda install pytorch torchvision torchaudio -c pytorch

# just upgrade all the modules... 
conda install -c anaconda chardet
conda install -c conda-forge tqdm
conda install -c conda-forge torchmetrics=0.6.0
# Did not manage to figure it out. going to create new env and restart


# No GPU on MacOS is slow.. trying to use accelerated GPU
conda install pytorch torchvision -c pytorch-nightly
conda install jupyter pandas numpy matplotlib scikit-learn tqdm 

https://github.com/mrdbourke/pytorch-apple-silicon
https://www.youtube.com/watch?v=Zx2MHdRgAIc
https://lightning.ai/docs/pytorch/stable/accelerators/mps_basic.html 
https://developer.apple.com/metal/pytorch/

# to remove a conda env
- conda remove --name pytorch_nightly --all
- conda create -n pytorch_night python=3.8.0
- To fix the issue: https://stackoverflow.com/questions/62903775/-intel-mkl-error-using-conda-and-matplotlib-library-not-loaded-rpath-libiomp5 run the following command
conda install -c conda-forge llvm-openmp --force-reinstall

# there is no need for nightly version.. apparently mps is also available on the stable version now 
conda create --name pytorch_mps1 python=3.9 -y
conda activate pytorch_mps1
conda install pytorch::pytorch torchvision torchaudio -c pytorch
conda install pandas jupyter jupyterlab scikit-learn matplotlib -y
conda install pytorch-lightning tensorboard -y
conda install -c conda-forge torchmetrics
conda install dicom2nifti nibabel pydicom numpy -y
python -m ipykernel install --user --name=pytorch_mps1
conda list --export > requirements_mps1.txt

```If Lightning can’t detect the Apple Silicon hardware, it will raise this exception:

        MisconfigurationException: `MPSAccelerator` can not run on your system since the accelerator is not available.
    If you are seeing this despite running on an ARM-enabled Mac, the most likely cause is that your Python is being emulated and thinks it is running on an Intel CPU. To solve this, re-install your python executable (and if using environment managers like conda, you have to reinstall these as well) by downloading the Apple M1/M2 build (not Intel!), for example here.
```
Install Miniforge3 with the following steps
    Download Miniforge3 (Conda installer) for macOS arm64 chips (M1, M2, M1 Pro, M1 Max, M1 Ultra).
    Install Miniforge3 into home directory, Get from this link: https://github.com/mrdbourke/pytorch-apple-silicon 
    Run the following terminal commands
        chmod +x ~/Downloads/Miniforge3-MacOSX-arm64.sh
        sh ~/Downloads/Miniforge3-MacOSX-arm64.sh
    Restart terminal
        source ~/miniforge3/bin/activate
Make sure I can use the arm64 arch
https://towardsdatascience.com/python-conda-environments-for-both-arm64-and-x86-64-on-m1-apple-silicon-147b943ffa55
Run the following commands:
    conda create --prefix ./pytorch_arm64 python=3.9
    conda activate ./pytorch_arm64
    pip install -r requirements_mps_arm64.txt
Do not need to run python -m ipykernel install --user --name=pytorch_mps1
Make sure kernel is Python3 (ipykernel)
arch should now be arm64, and sys.executable should be /Users/marcusc/Desktop/MyRepos/DeepLearningwithPyTorchforMedicalImageAnalysis/pytorch_arm64/bin/python

