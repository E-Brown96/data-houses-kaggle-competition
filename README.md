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

<h5>Initial data cleaning</h5>
To generate a baseline score some basic data cleaning and processing was performed including; numerical and categorical features were split. Then the numerical features were accessed for correlation using a seaborn heatmap and those with a correlation greater than 0.7 were excluded. For categorgircal variables any variable with other 7 unique values was removed and the rest were one-hot-encoded.

<h5>Building a pipeline</h5>
Following the initial clean up of the data a pipeline was constructed. The numerical data was imputed using the mean strategy of the simple imputer and then scaled using the MinMaxScaler. The categorical values were one-hot encoded and imputer with the most frequent value. Both were put into a column transformer to form the final preprocessing pipeline.

<h5>Baseline model</h5>
Upon completion of the initial preprocessing pipeline a baseline model was generated using this pipeline and a Decision Tree Regressor model from sklearn. To score the model kaggle required the use of the root mean squared log error, which is not readily available as a metric so a function was created to determine the score.

<h5>Improving the model</h5>
A number of iterations were performed on the data to try and improve the score of the model including:
- Ordinal encoding some of the categorical features and adding this to the pipeline
- Using Univariate, multivariate and variance threshold to help eliminate features that were causing the model to overfit and did not help predict the target.
- Custom functions were added to remove correlated features and to convert the time in months to a cyclical feature using sine and cosine

<h5>Final model</h5>
The final model was then saved to a csv file and this csv file uploaded to kaggle to determine the final score of the best model, which was 0.20.
