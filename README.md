# MovieGenrePrediction

Movie Genre Prediction uses predictive analytics to predict multiple genres associated with a movie plot. 
Logistic Regression is used for classification along with several feature engineering techniques like CountVectorizer,TF-IDF and Word2Vec.

The test.csv and train.csv are the data files. Thanks to CMU for the data set.

TFIDFPredictions.csv - Predictions generated using TFIDF feature engineering technique.
TermDocumentMatrixPredictions.csv - Predictions generated using TDM feature engineering technique.
Word2VecPredictions.csv - Predictions generated using Word2Vec feature engineering technique.

Here is a brief summmary of how this was achieved.

Procedure:

1.	Create a Spark Session and build a Spark Context. 
2.	Using the SQL Context, we read the train and test files and load them into PySpark dataframe.
3.	We clean the plot column in the dataframe by removing any special/unwanted characters. 
4.	We remove the stop words from the clean plot column. 
5.	We load the mapping file data into a dataframe and generate a list of genres that we need to predict. Using this list, we create one column for every genre from the train file (example. genre_Drama, genre_Comedy etc.). These columns contain 1 if the genre is present for that particular movie/row else 0. 
6.	We use the Tokenizer function of PySpark library and tokenize the sentences in the plot column. 
7.	The output column of the Tokenizer function is fed as the input to the CountVectorizer/Word2Vec/TF-IDF function to generate the feature vectors.
8.	We repeat the steps 3 to 7 for the test data as well. 
9.	We treat this multilabel classification problem as combination of 20 different binary classification problems training over each genre individually. These trained models for each genre are used to predict the genre level output labels for that test data. 
10.	We join all the predictions into test dataframe using inner join. 
11.	We use the SQL command to combine the multiple predictions columns into the desired format which is in csv format. 
