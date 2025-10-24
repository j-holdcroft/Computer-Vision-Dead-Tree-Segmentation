# 9517-GroupMouse
Finding dead trees
| Name:     | zID:      |
|-----------|-----------|
| Arki      | z5421196  |
| Daniel    | z3543817  |
| Jamie     | z5591952  |
| Kateryna  | z5562576  |
| Max       | z5592844  |



** some placeholder titles: **
## Method 1: Rule-based image processing
We implemented a fast, interpretable rule-based pipeline using classical computer vision techniques to detect dead trees in NRG imagery. The approach removes non-forest areas using red and green thresholds, normalises color intensities, and applies fixed rules to identify dead vegetation based on spectral properties—specifically high red and low green reflectance. Morphological operations refine the output, producing binary masks of dead-tree candidates. While not as precise as learning-based methods, this approach provides a strong lightweight baseline with no training required.

## Method 2: Feature extraction and machine learning

From the images superpixel regions are extracted. For each of the superpixel regions, features of that region are extracted, specifically a 13 dimensional vector where:
Index 0,1,2,3 are used to store the (mean) red, green, blue and NIR pixel values, 4 stores the mean NDVI (μ) while 5, 6, 7, 8, 9 stores standard deviation (σ) in NDVI, red, green, blue, NIR. 6 stores the red pixel value standard deviation (σ). 10 segments relative area (basically stores how big the super pixels are). 11 extracts branch/shadow texture. 12 extracts the GLCM entropy.

Machine learning is done via a Random Forest Classifier on the 10 dimensions for each superpixel, with a with the listed features extracted from the dataset. (hyperparamers were be varied but default set at: 
        n_estimators=400,
        class_weight='balanced', 
        n_jobs=-1,
        random_state=42).

## Method 3: Deep learning
The deep learning method chosen for solving this problem is U-Net based NN.
The solution notebook includes dataset preprocessing, data cleanup, resizing and normalization,
dataset split (80/20).
Also there were 2 models implemented (the custom simplified U-Net based model and the imported one from smp module), 2 different loss functions and several values of the learning rate for Adam optimizer. 
To choose the best perfroming combination, the models were trained on half of the dataset, so that the best model was selected and trained.
The model was tested on multiple sample examples. 

## Other notes:
### Venv Activate/deactivate
- To create: python -m venv .venv
- To activate: source .venv/bin/activate
- To deactivate: deactivate

### Dependencies
Once the venv is active run:
pip install -r ./requirements.txt
