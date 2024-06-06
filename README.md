# deeptaskgen-models
This repository contains trained DeepTaskGen models on various open datasets. These models can predict task contrast maps from voxel-to-ROI resting-state connectivity data. Instructions for preparing the input data can be found here: https://github.com/eminSerin/deeptaskgen-paper. 

The models are trained on the following datasets:

1. **Human Connectome Project Young Adult (HCP-YA):** The main model, serving as the pre-trained model for other datasets, was initially trained on this dataset (Date: 20/09/2023). The model is available at `hcp-ya/main_model_200923.ckpt`, and it can predict [47 different task contrast maps](misc/hcp-ya_contrasts.txt). 

2. **Human Connectome Project Development (HCP-D):** The pre-trained model (on HCP-YA) was fine-tuned using the EMOTION FACES-SHAPES task (Finetuning Schedule 1, Date: 02/10/2023). The model is available at `hcp-d/finetuned_model_021023.ckpt`, and it can predict [47 different task contrast maps](misc/hcp-ya_contrasts.txt).

3. **UK Biobank (UKB):** The pre-trained model (on HCP-YA) was fine-tuned on this dataset using the EMOTION FACES-SHAPES task (Finetuning Schedule 1, Date: 10/10/2023). Access the model at `ukb/finetuned_model_021023.ckpt`. It can predict [47 different task contrast maps](misc/hcp-ya_contrasts.txt).

Model configurations are stored in the `config.yaml` file within each dataset directory.

### Finetuning
We employed two different fine-tuning procedures depending on the datasets: 
- **Schedule 1:** Used when there are common tasks between the HCP-YA dataset and the target dataset. The output layer was frozen, and only the remaining layers (backbone) were fine-tuned using MSE loss.
- **Schedule 2:** Utilized when there are no common tasks between the HCP-YA dataset and the target dataset. The output layer was replaced with a new one, and the entire model was fine-tuned using MSE loss.

### Usage
You need to install the DeepTaskGen package to use the models. The package can be accessed at https://github.com/eminSerin/DeepTaskGen. To predict task contrast maps using the models, refer to the [`deeptaskgen/predict.py`](https://github.com/eminSerin/DeepTaskGen/blob/main/deeptaskgen/predict.py) script.

