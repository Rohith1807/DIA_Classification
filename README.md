# DIA Prediction - User Manual

This project includes application of several machine learning models to predict a given drug's susceptiblity to producing drug-induced autoimmune disorders in partients based on its molecular properties. For this purpose, a Logistic Regression, RBF SVM, Random Forest, Gradient Boosting Classifier, Bagged Tree Classifier, and Ensemble of all the aforementioned models are developed and trained against the following Drug Induced Autoimmunity Prediction dataset from the UCI machine learning repository accessible at the following link: https://archive.ics.uci.edu/dataset/1104/drug_induced_autoimmunity_prediction

The machine learning modeling efforts executed for this study included development of a standard flow, including a data pre-processing pipeline to prepare the training and testing data in a consistent manner for evaluation by all models developed. This process consisted of the following main steps: 

  1. Data pre-preprocessing pipeline
     - Optional outlier removal
     - Optional regularization (L1)
     - Optional usage of ONLY MACCS fingerprints
     - Optional binning of numerical predictors
  2. Model hyperparameter search and selection, and model probability prediction threshold tuning via cross-validation
  3. Model training and performance against training set from the cross-validation process
  4. Model performance assessment against test set data
  5. Feature importance assessment
  6. Optional feature removal and re-assessment of model performance

Several runtime switches are provided within the Jupyter notebook; the motivation is to provide switches for experimentation to observe model performance and output with varying datapreprocessing steps applied among other parameters and conditions. These switches and are as follows and are listed with their respective default values as configured in the notebook:

  - kf = 3 : Number of folds for initial regularization and cross-validation
  - sel_max_score = False : Flag to indicate if maximum score alpha should be selected for the LogisticRegressionCV
  - num_predictors_to_sel = 250 : Number of predictors to keep for regularization if not using the maximum score alpha
  - use_smiles = True : Flag to enable usage of SMILES strings to generate MACCS keys and utilize the bits as CAT vars for DIAD prediction
  - random_state = 0 : Random state for reproducibility
  - reeval_imp_features = True : Switch to enable reevaluation of model performance after removal of unimportant features, potentially hurtful to model performance as determined by permutation importance analysis with cross validation on the TRAINING data set (zero or negative score features with zero standard devation are removed)
  - use_only_maccs = False : Optional switch to use ONLY MACCS fingerprint CAT variables to train the models
  - en_num_var_binning = True : Optional switch to enable binning of numerical variables to train the models
  - n_bins = 3 : Optional number of bins to use for binning of numerical variables

The datapreprocessing pipeline method, feature_preprocess() additionally contains several switches to enable/disable certain pre-processing features and are as follows listed along with default values where applicable:

  - en_reg = False : Flag to enable CV regularization with Logistic Regression to filter out 'useless' features. This will conduct a (default 3) kf-fold cross-validation regularization and select a lambda value corresponding to the roc_auc score within 1 standard error of the maximum score
  - en_outlier_removal = True: Flag to enable outlier removal with OneClassSVM()
  - bin2cat = True: Flag to enable conversion of binary variables to categorical vars

# Configuring Environment and Running the Script:

The Jupyter notebook written for this project was intended for use in Google Colab. To run the script, two alternative approaches may be employed. The dataset and Jupyter notebook are accessible at the following OneDrive Link: https://uofstthomasmn-my.sharepoint.com/:f:/r/personal/delg5279_stthomas_edu/Documents/SEIS%20763/Semester%20Project/Project%20Zipped%20Files?csf=1&web=1&e=aegNYG

To run the script, copy the Jupyter notebook file (DIA_Classification.ipynb) to Google Drive under your desired directory/path of choice. The dataset files for processing by the machine learning models are also provided in the OneDrive link. These should be copied to the same directory/path as the Jupyter notebook. Before running the script, the paths to the training and testing datasets must be set correctly in the Colab Notebook. Modify the following lines of code in the runtime switch and helper function cell (2nd code cell) to include the path where the dataset files have been placed:

<img width="1053" height="73" alt="image" src="https://github.com/user-attachments/assets/61132d23-4fee-4adb-acc6-2e16cda3e3c8" />

Once the paths have been configured correctly, the dataset may be loaded, and the script may be run. Open the Jupyter notebook which has been copied to OneDrive, and click "Run all" in the Google Colab environment to allow the script to run.

