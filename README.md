# **Identifying Nutrient Deficiencies in Satellite Farmland Imagery**
## by [mr-steven-tran](https://github.com/mr-steven-tran)

---

### Welcome!
This is the repository for my project **Identifying Nutrient Deficiencies in Satellite Farmland Imagery**. In this project, I train a U-Net Convolutional Neural Network to perform semantic segmentation on satellite farmland RGB and near-infrared imagery. You can read about the project background and motivation, exploratory data analysis, modeling process, and results in my [Executive Summary](executive_summary.md).

---

### Getting started

If you're interested in reproducing my work, please start with retrieving the requisite data, a process which is outlined in [Data Retrieval and Model Training](Data_Retrieval_and_Model_Training.md). Reproduction of my process should occur in the following steps, involving the below notebooks:

|Step|Description|Notebook|
|----|-----------|--------|
|1|Download the dataset|N/A, follow steps in [Data Retrieval and Model Training](Data_Retrieval_and_Model_Training_Setup.md)|
|2|Filter the dataset|[00_Data_Retrieval.ipynb](code/00_Data_Retrieval.ipynb)|
|3|Conduct Exploratory Data Analysis|[01_EDA.ipynb](code/01_EDA.ipynb)|
|4|Prepare data for modeling|N/A, follow steps in [Data Retrieval and Model Training](Data_Retrieval_and_Model_Training_Setup.md)|
|5|Model using Google Colab|[02A_UNET_RGB_Model_Training.ipynb](code/02A_UNET_RGB_Model_Training.ipynb) and [02B_UNET_Multispectral_Model_Training.ipynb](code/02B_UNET_Multispectral_Model_Training.ipynb)|
|6|Evaluate the trained models|[03_Model_Evaluation.ipynb](code/03_Model_Evaluation.ipynb)|

---

### Works Cited

* AgricultureVision was accessed on December 10, 2021 from https://registry.opendata.aws/intelinair_agriculture_vision. 

* "U-Net: Convolutional Networks for Biomedical Image Segmentation" (https://arxiv.org/abs/1505.04597)