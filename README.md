<img src='https://wagon-public-datasets.s3.amazonaws.com/data-science-images/ML/kaggle-batch-challenge.png' width=600>

Below are the instructions I recieved from my bootcamp:

Welcome to your first Kaggle Competition!

<h3>Instructions</h3>

Your objective is to **submit online an answer** to the open competition 🔥

Your whole class will compete as a group against the team of TAs!

Download the datasets in the `data` folder and upgrade `sklearn` to its latest version

```bash
cd ~/code/<user.github_nickname>/{{local_path_to("05-ML/07-Ensemble-Methods/01-Houses-Kaggle-Competition")}}
curl https://wagon-public-datasets.s3.amazonaws.com/houses_train_raw.csv > data/train.csv
curl https://wagon-public-datasets.s3.amazonaws.com/houses_test_raw.csv > data/test.csv
curl https://wagon-public-datasets.s3.amazonaws.com/houses_sample_submission.csv > data/sample_submission.csv
pip install --upgrade pip
pip install --upgrade scikit-learn
```

Open `houses_kaggle_competition.ipynb` and follow instruction

<h3>Objective</h3>

The objective of this task was to analyse the dataset provided by kaggle. The jupyter notebook file is very detailed with all steps clearly explained, however I have also included all the steps taken under the headers below.

<h5>Loading the dataset</h5>
This dataset was already split into train and test and just had to be loading from a csv file.

<h5>Splitting the dataset</h5>
Next the larger (non-test) dataset was split into a train and validation set.

<h5>Preprocessing the data</h5>
In a previous challenge we had created a pipeline which did the following:
- For numerical values a KNNImputer was used followed by a MinMaxScaler
- For all categorical values a simple imputer was used
- The values were then split with some being ordinal encoded and others being one hot encoded
- Finally these categorical (now numerical) values were scaled using the MinMaxScaler

As this was done in a previous challenge the pipeline in this notebook was imported and fitted to the X_train and y_train values. It was then used to transform the X_train, y_train and X_val datasets. 

<h5>Predictions using Tensorflow/Keras</h5>
Once the data was prepared a regression could be performed on the dataset using the Keras library. The metric used to measure the model was specified on Kaggle as the RMSLE (root mean square log error). 

The instantiated model was a Sequential model and 12 different layers were used, these were all dense layers with relu chosen as the activation. As it was a linear regression for the final layer linear was chosen as the activation.

The model was then compiled using the adam optimser a loss measured using msle and the metrics chosen as msle.

The model was fit using a batch size of 32 and 150 epochs, then the results were evaluted (Note the loss and metric variables were square rooted to get the rmsle). The history of the loss was also plotted against the number of epochs for train and validation to get a sense as to whether the model was overfitting or underfitting. 

<h5>Submitting to Kaggle</h5>
To submit my final model results to kaggle, the model predicted the values of y using X_test then a results dataframe was created and exported to a csv file which could then be uploaded to kaggle. 
