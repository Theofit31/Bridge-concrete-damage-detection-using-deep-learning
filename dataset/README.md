Dataset
This project uses the CODEBRIM (COncrete DEfect BRidge IMage Dataset) for multi-label classification of concrete bridge damage.
Official Dataset
The dataset can be downloaded from the official Zenodo repository:
https://zenodo.org/records/2620293
Please download the appropriate CODEBRIM classification dataset from the official source.
Damage Classes
The project uses five damage classes:
- Crack
- CorrosionStain
- Efflorescence
- ExposedBars
- Spallation
Expected Directory Structure
After downloading and extracting the dataset, the directory should be organized as follows:
dataset/
└── building/
    ├── train/
    │   ├── Images/
    │   └── Labels/
    │
    ├── valid/
    │   ├── Images/
    │   └── Labels/
    │
    └── test/
        ├── Images/
        └── Labels/
The notebook uses these relative paths:
dataset/building/train
dataset/building/valid
dataset/building/test
Each split contains an Images folder for image files and a Labels folder containing the corresponding label files.
Important Note
The original dataset is not included in this GitHub repository because of its large size and dataset usage conditions.
Download the dataset directly from the official source and place it in the directory structure described above before running the notebook.
Reference
Mundt, M., Majumder, S., Murali, S., Panetsos, P., & Ramesh, V. (2019).
Meta-learning Convolutional Neural Architectures for Multi-target Concrete Defect Classification with the COncrete DEfect BRidge IMage Dataset.
IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR).
