## Electron Microscopy Semantic Segmentation 

The electron microscopy dataset by Lucchi et al.[1] (https://www.epfl.ch/labs/cvlab/data/data-em/) has been used to perform 3D semantic segmentation. The dataset represents a  5x5x5µm section taken from the CA1 hippocampus region of the brain, corresponding to a 1065x2048x1536 volume. The resolution of each voxel is approximately 5x5x5nm. The data has two subvolumes: a training subvolume and a testing subvolume. Each subvolume has a corresponding ground truth subvolume with annotated mitochondria. The size of a subvolume is 165x768x1024 (z*h*w). The particular dataset is considered a benchmark dataset for mitochondria segmentation. 

Here, we implement a basic 3D U-Net model for the semantic segmentation task. As the original subvolume is too large to be fed directly into the model, the subvolumes are converted to smaller patches using the ‘crop_3D_data_with_overlap’[overlap= (0,0,0)] function from the BiaPy library[2]. This produces 390 patches of each subvolume of size 80x80x80. 

The model is implemented using PyTorch. The loss is calculated using Binary Cross Entropy loss and minimised through the Stochastic Gradient Descent optimiser with a learning rate of 0.002 (parameters from Franco-Barranco et al. [3]).  The model is trained only for 10 epochs due to computational constraints. The test dataset achieves an average accuracy of 0.9475 with an average intersection over union (IoU) of 0.5045. 

<img width="429" alt="Screenshot 2025-04-17 at 8 31 42 PM" src="https://github.com/user-attachments/assets/8e49fca2-1bc2-4397-a75e-c17379ac5535" />
<img width="487" alt="Screenshot 2025-04-17 at 8 32 47 PM" src="https://github.com/user-attachments/assets/1bf5a79b-5d99-49ac-97f4-26329068e284" />

### References

1.	Lucchi, A., Smith, K., Achanta, R., Knott, G. & Fua, P. Supervoxel-based segmentation of mitochondria in em image stacks with learned shape features. IEEE Trans. Med. Imaging 31, 474–486 (2012).
2.	Franco-Barranco, D. et al. BiaPy: a ready-to-use library for Bioimage Analysis Pipelines. in 2023 IEEE 20th International Symposium on Biomedical Imaging (ISBI) 1–5 (2023). doi:10.1109/ISBI53787.2023.10230593.
3.	Franco-Barranco, D., Muñoz-Barrutia, A. & Arganda-Carreras, I. Stable Deep Neural Network Architectures for Mitochondria Segmentation on Electron Microscopy Volumes. Neuroinformatics 20, 437–450 (2022).
