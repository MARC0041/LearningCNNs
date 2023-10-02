# Neuroimaging
Resource: https://www.andysbrainblog.com/


1. After scanning in MRI, you will either have some kind of `.mgz` file or `.dcm` dicom file. You should then convert it to a compressed nifti file for analysis in freesurfer. Conversion to .nii.gz file can be done via this tutorial: https://www.youtube.com/watch?v=DMGWdi6Z73s&t=300s 
    - MRIcroGL software is used to convert the files. 
    - If your files are `.mgz`, you can use mri_convert command from freesurfer.  
    - Running Freesurfer using terminal: 
        - First the setup for freesurfer: https://www.youtube.com/watch?v=BSQUVktXTzo&list=PLIQIswOrUH6_DWy5mJlSfj6AWY0y9iUce&index=3 
            ```
            export FREESURFER_HOME=/Applications/freesurfer
            source $FREESURFER_HOME/SetUpFreeSurfer.sh
            export GROUPH="/Users/marcusc/Desktop/MyRepos/Freesurfer Subjects/Group_H"
            export GROUPMCI="/Users/marcusc/Desktop/MyRepos/Freesurfer Subjects/Group_MCI"
            cd $GROUPH
            ```
        - Next, go to bash in terminal with : `bash` and you should see `bash-3.2$ `.
        - Now check you are in the correct path using `ls` 
            - SKIP THIS STEP AND DO NOT DO THIS! FOR SOME REASON WHEN SUBJECTS_DIR is NOT IN APPLICATIONS/freesurfer, the parallel recon-all cannot run!!!!!! MAKE SURE SUBJECTS_DIR is the original subjects folder. 
        - 
            ```
            export SUBJECTS_DIR_H=`pwd` 
            echo SUBJECTS_DIR_H 
            ``` 
        - Run the parallel command: https://andysbrainbook.readthedocs.io/en/stable/FreeSurfer/FS_ShortCourse/FS_04_ReconAllParallel.html 
            - Check number of cores: ```sysctl hw.physicalcpu hw.logicalcpu```. You can then run the following command
            - Install parallel using ```brew install parallel ```
            - Running the parallel command. Make sure subj dir is changed because that is where the files will be outputted. 
                ```
                export SUBJECTS_DIR=`pwd`
                echo $SUBJECTS_DIR
                ls *.nii | parallel --jobs 8 recon-all -s {.} -i {} -all -qcache
                ```
                This command runs the pre-processing step using recon-all for the nifti files in the folder in parallel
        - For some reason the above command creates empty folders. Trying something else now... 
            ```
            recon-all -s bert -all
            ```
        - freeview from FreeSurfer


2. Go into the folder with the group of nifti files in the terminal. `cd $CONTROL_GROUP`. Then run the command `recon-all -s bert -all` to perform a recon-all command on the existing folder
    - freesurfer version used is installed from 7.1.1 and installed from .tar.gz file. Keep in mind that you need to also change develop settings in mac so that you can run freesurfer commands from terminal
    - Also need to download the license from this website. and put it into freesurfer folder. https://surfer.nmr.mgh.harvard.edu/fswiki/License 
3. SKIP running recon-all for individual samples since we want to do group analysis
4. Running recon-all in Parallel: https://www.youtube.com/watch?v=XHN2tm3tNaw&list=PLIQIswOrUH6_DWy5mJlSfj6AWY0y9iUce&index=4




# Trying 7.1.1 pkg file again and set default terminal to bash
1. https://www.youtube.com/watch?v=P2_sbNFvCek
2. Run the following command and restart terminal
```
chsh -s /bin/bash
```
3. Set up freesurfer, and cp subjects folder to Desktop for read/write access.
```
export FREESURFER_HOME=/Applications/freesurfer/7.1.1
cd $FREESURFER_HOME
cp -r subjects ~/Desktop
cd
export SUBJECTS_DIR=$HOME/Desktop/subjects
source $FREESURFER_HOME/SetUpFreeSurfer.sh
``````
Trying recon-all for one sample: 
`/Users/marcusc/Desktop/MyRepos/FreesurferSubjects/Group_H/002_S_1280/Accelerated_Sagittal_MPRAGE/2017-03-13_13_38_31.0/I829296/ADNI_002_S_1280_MR_Accelerated_Sagittal_MPRAGE__br_raw_20170314122249698_141_S545524_I829296.dcm`

Issue found: Note that there should be no spaces in your path! IF there are spaces, recon-all will fail. see https://www.mail-archive.com/freesurfer@nmr.mgh.harvard.edu/msg71597.html
```
cd /Users/marcusc/Desktop/MyRepos/Freesurfer Subjects/Group_H
mri_convert "002_S_1280/Accelerated_Sagittal_MPRAGE/2017-03-13_13_38_31.0/I829296/ADNI_002_S_1280_MR_Accelerated_Sagittal_MPRAGE__br_raw_20170314122249698_141_S545524_I829296.dcm"
```
Try for `Healthy_Controls_copy_Accelerated_Sagittal_MPRAGE_20170313133831_2.nii`

# install brew
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

echo 'eval $(/opt/homebrew/bin/brew shellenv)' >> /Users/marcusc/.zprofile

eval $(/opt/homebrew/bin/brew shellenv)

brew install parallel
```

# Try parallel recon-all again
1. Run command: 
```
ls *.nii | parallel -jobs 8 recon-all -s {.} -i {} -all -qcache
ls *.nii | parallel -j 8 recon-all -s {.} -i {} -all -qcache

```