# DNN - UCSF Brain Networks Lab

**PI:** Ashish Raj, PhD.

**Project Lead (Forward Prediction) :** Samuel Wollenburg

**Project Lead (Initial Seed Prediction) :** Sarah Gomez

**Contributors/Advisors :** Daren Ma, MSc.,  Justin Torok, PhD.

**Description :** This project contains a Deep Neural Network to both predict the initial seed location and the forward progress of tau tangle concentration in the brain.

## Subdirectories 

- `data/` : Contains datasets that are ordered and normalized, including merged tau demographics and Nexis seed predictions.
** Note on `data/` folder**
We decided to omit the data contained in this folder to adhere to patient privacy. To access similar datasets, create an account with the [Alzheimer's Disease Neuroimaging Initiative (ADNI)](https://adni.loni.usc.edu/) or download similar datasets containing tau concentrations per region and patient demographics. In such cases, use `data_modification_2b` as a template to modify your own dataset.


## Files

- **Data Modification in `data_modification_2b.ipynb`**:
        - The script calculates the average tau values between the left and right cerebellum cortex and normalizes the left and right cerebellum cortex in  **`Tau_with_Demographics.csv`**: values by subtracting this average, setting any negative results to zero. It also reorders columns alphabetically and performs min-max scaling on the `ml_stage`.
        - **Categorical Binning and Encoding**: Age and years of education are binned into categorical ranges, and columns like gender and cognitive scores are one-hot encoded.
         - **`connectome_mean80_fibercount.csv`**: Columns are reordered alphabetically. The script also drops columns that are missing from another specified DataFrame. 
        - **`Seeding patterns.csv`**: The script performs similar operations on this dataset as on others. It reorders columns alphabetically and checks for duplicates based on the `RID` column. The script also compares and ensures that the `RID` values in this dataset match those in the demographic data to maintain consistency across merged datasets. Additionally, columns starting with 'Unnamed' are dropped to clean up the data.        
        - **Merging DataFrames**: `Tau_with_Demographics.csv` and `Seeding patterns.csv` are merged based on the `RID` field, ensuring an inner join that excludes unmatched records.
        - **File Outputs**: Saves final datasets, such as reordered connectome data and merged datasets, ensuring that data integrity and consistency are maintained across operations.


- **Physics Informed Neural Network in `DNNTau.ipynb`**:
    - This script focuses on the development and implementation of a Physics Informed Neural Network (PINN) to predict the initial seeding and progression of tau protein in the brain. It includes the creation of the neural network model, preprocessing steps to prepare input data from demographics and connectome datasets, and the execution of training and validation processes using cross-validation techniques.
    - **Model Definition and Initialization**: Defines the `TauPINN` class that incorporates neural network layers tailored to predict both tau propagation and the associated times of progression based on input features derived from brain imaging and demographic data.
    - **Training and Evaluation**: Implements training sessions using custom loss functions that integrate mean squared error and optional L1 regularization. It provides detailed evaluation metrics such as Dice scores and correlation coefficients for both training and testing phases, alongside visual plots to track the performance over epochs.
    - **Cross-Validation Framework**: Utilizes a K-fold cross-validation approach to ensure the model's robustness and generalizability, with detailed outputs for each fold, including loss and accuracy metrics, and final testing on a separate test dataset.
    - **Predictive Outputs**: The script includes functions to extract and display predicted initial tau concentrations across different brain regions, providing insights into potential areas of highest tau accumulation.
  

- `README.md `: This file.


## Steps To Run

Step 1: Run data_normalization.ipynb to generate datasets

Step 2: Run PINN_forward.ipynb.
