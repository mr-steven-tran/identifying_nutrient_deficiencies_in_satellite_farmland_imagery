# **Identifying Nutrient Deficiencies in Satellite Farmland Imagery**
## Data Retrieval and Model Training Setup


The dataset for this project comes from the 2020-published [AgricultureVision dataset](https://registry.opendata.aws/intelinair_agriculture_vision/). This dataset is publicly accessible on the **Registry of Open Data on AWS** (Amazon Web Services). The subset of that dataset used in this project are the **14,712 images taken in 2018** having **nutrient deficiency** annotations. 

As the dataset is on the larger side (~3GB of disk space taken), the steps in this checklist must be taken before EDA and Modeling can be accomplished. This is due to two reasons:
* The dataset is too large to be hosted on base GitHub
* The modeling takes too long on CPU alone, so this analysis employs Google Colab and GPU acceleration to make training the models more efficient.

This checklist will be organized into two parts:
1. **Dataset Retrieval from Registry of Open Data on Amazon Web Services**
1. **Preparing for U-Net model training in Google Colab**

---

### **Dataset Retrieval from Registry of Open Data on Amazon Web Services**

**Checklist**:  
1.  Because the dataset was so large, the `data/` folder in root directory of the repository was omitted from the git push. Create that directory, `data/` now. Further, create the following subfolders in the `data/` directory: `data/features/`, `data/nir_features/`, and `data/labels/`.
1.  Depending on your machine's operating system, follow the instructions for how to [Install the latest version of AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) (Command Line Interface).
1.  Using **bash** or **terminal**, change your working directory to wherever you'd like the data downloaded. This may be in the cloned project repo if you've cloned it or another location of your chosing.
1.  Then, run the following commands in your shell:
    * *(Copies the `data2018_splits.json` file from AWS to your current directory, keeping the same filename)*: `aws s3 cp s3://intelinair-data-releases/agriculture-vision/cvpr_paper_2020/Dataset/data2018_splits.json data2018_splits.json --no-sign-request` 
    * *(Copies the `data2018_miniscale.tar.gz` file from AWS to your current directory, keeping the same filename)*: `aws s3 cp s3://intelinair-data-releases/agriculture-vision/cvpr_paper_2020/Dataset/data2018_miniscale.tar.gz data2018_miniscale.tar.gz --no-sign-request`
    * The second download in particular may take some time, depending on your download speeds
1.  Using a compression tool like [win-rar](https://www.win-rar.com/start.html?&L=0) or [7-zip](https://www.7-zip.org/), extract the contents within the `data2018_miniscale.tar.gz` file to the **root directory of the project repository**. The uncompressed directory structure for the 2018 AgricultureVision dataset should look like the following:

```
repository_root_directory/
  --code/ <--- where all the repo .ipynb files are
      --00_Data_Retrieval.ipynb
      ...
  ...
  --data/
      --features/
      --nir_features/
      --labels/
  --data2018_miniscale/
      --field_bounds/
      --field_images/
      --field_labels/
      --field_masks/
      --field_stats.json
      --split_stats.json
      --stats.json
```

If up to this point, your directory structure looks like the above, you are then clear to run the [Data Retrieval notebook](code/00_Data_Retrieval.ipynb).


---

### **Preparing for U-Net model training in Google Colab**


**Checklist**:  
1.  Before proceeding down this checklist ensure that the following notebooks have been run:
    * [Data Retrieval](code/00_Data_Retrieval.ipynb), in which only the **nutrient deficiency**-labeled images are extracted from the 2018 image set, and
    * [EDA](code/01_EDA.ipynb), in which we apply some clustering and assign each of the images in the dataset to a cluster and track the assignments in [image_metadata_with_clusters.csv](data/image_metadata_with_clusters.csv).
1.  Using a compression tool like [win-rar](https://www.win-rar.com/start.html?&L=0) or [7-zip](https://www.7-zip.org/), add the contents of each of the following file folders to a **.zip** file. This file extension is **critical** because the Google Colab notebooks are set up to expect a zip file with a specific name.  
    Folders to compress to `.zip` format:
    * `repository_root_directory/data/features` -> `features.zip`
    * `repository_root_directory/data/nir_features` -> `nir_features.zip`
    * `repository_root_directory/data/labels` -> `labels.zip`
1.  Upload `features.zip`, `nir_features.zip`, and `labels.zip` to Google Drive (you will need to sign into your Google account to do so). Ensure it is in a directory you can access through Colab.
1. Upload the [UNET RGB Model Training](code/02A_UNET_RGB_Model_Training.ipynb) and [UNET_Multispectral Model Training](code/02B_UNET_Multispectral_Model_Training.ipynb) notebooks to Google Colab.
1.  Update the `gdrive_path` variable in the notebooks [UNET RGB Model Training](code/02A_UNET_RGB_Model_Training.ipynb) and [UNET_Multispectral Model Training](code/02B_UNET_Multispectral_Model_Training.ipynb) with the directory path containing the three `.zip` files you uploaded above.

If all steps in the checklist were followed up to this point, then you should be able to run both modeling notebooks, [UNET RGB Model Training](code/02A_UNET_RGB_Model_Training.ipynb) and [UNET_Multispectral Model Training](code/02B_UNET_Multispectral_Model_Training.ipynb).

As detailed in those notebooks, the outputs of the modeling process is a set of model weights that can be loaded in the final notebook [Model Evaluation](code/03_Model_Evaluation.ipynb). Follow the instructions left in the comments of those notebooks and download the output `.h5` model weights to the `repository_root_directory/output/best_model_weights` folder.


