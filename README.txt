Андрей,
отправляют Вам данные по тестовому заданию.

Задача: Повторить исследование, описанное в работе Forecasting the Stock Market using News Sentiment Analysis (прилагается), и предоставить результаты двух прогнозов (по каждому, accuracy и confusion matrix), полученные с использовании:
1.    SVM, TextBlob.
2.    SVM, TextBlob+TA.
 
Дать оценку данной работе в виде короткого эссе (достоинства, недостатки, ошибки, рекомендации).
 
Материалы:
1. Forecasting the Stock Market using News Sentiment Analysis. Прилагается.
2. Dataset YahooFinancials package. Прилагается.
3. Dataset “all-the-news-2-1”. Скачать здесь - https://components.one/datasets/all-the-news-2-news-articles-dataset/.
 
Срок выполнения 5 дней - к 28 июля 12:00.
Вознаграждение 15,000 р. вне зависимости от того, сможете ли Вы достигнуть показатели, описанные в работе. Мы ценим время людей, с которыми работаем.
 
С уважением
Ольга Летунова
+7 (981) 8480579
ООО Рестадвайзер
Телефон, Telegram, WhatsApp
--------------------------
http://smartventures.pro



* Why only SVM?
* How the data and the stocks were chosen?    daily S&P 500 index movements
* How representitive are they?
* Is this prediction for the whole market or for individual stocks?
* Analysis on the basis of news is not allways a good idea, especially, if the news concern insider information - insider trading
	* often, if a news came out, its too late to "jump on the trend"
* The researcher has chosen to filter out the article text because his computer was not able to execute any of the sentiment analysis methods on the whole article text. Therefore, the title of the article will be considered to represent the news article sentiment.
* Since the prediction of a stock for the following day is considered as a short-term prediction, the period should is set on 10 days
	* to long term/middle term/short term and the ensemble learning (majority vote)
* if some days are skipped (are they), do we take the previous existing 10 days or e.g. the last 8 days, if 2 days from the last 10 were skipped?



News articles preprocessing (all-the-news-2-1.csv):
* keep date, title, section, and publication. 
* skip article text
* all the rows without a title are filtered to assure that each entry has a filled title column
* Some publishers do not have a filled section column; these entries are replaced with “unknown”. However, this study is mainly focused on financial and business news articles and with an “unknown” section column it is impossible to decide whether it belongs to a financial and business article or not. Therefore, this study uses two news article datasets, (1) with all the news articles with a financial or business-related section, and (2) all the news articles with unknown sections combined with dataset 1.

News Articles Sentiment Scores
* After preprocessing the news article dataset, some code should be executed to gather the different sentiment score features. As mentioned in Section 3.2 the following sentiment scores are calculated and added to the two news articles datasets: VADER, TextBlob, and LM. Hence, each row (news article) has several sentiment score columns. Since the news article and price datasets will be merged on the date columns, a group by date function has been executed. While grouping the rows by the date column, the sentiment scores will be averaged.


S&P 500 preprocessing (YahooFinancials package.xls) (1785 entries before preprocessing, includig keys row)
* keep columns: close price, volume, and date
* Another column has been added with the movement, this is de binary dependent variable in this study. A 1 is assigned if the stock market value went up or remained the same compared to the day before and 0 if the stock market values went down.
* Since it has been decided to use fundamental as well as technical analysis, a column has been added with a technical indicator. Although there are many technical indicators which can be calculated with the features in the S&P 500 dataset, the most common one has been chosen, which is the simple moving average (SMA). To calculate the SMA, all the closing prices are summed up over a given period and divided by the number of periods
SMA = (A1 + A2 + ... + An) / n
* Since the prediction of a stock for the following day is considered as a short-term prediction, the period should is set on 10 days


Merge Datasets:
* After the datasets are preprocessed, the price dataset has been left joined to the news article datasets to create two datasets that will be used as input and output for the machine and deep learning models. 
* The datasets are merged on the column date. Thus, the two dataset which will be used for this research are fully preprocessed and both contains 1,096 rows. Because both datasets consist of the same features only one table has been created to give an overview of all the features in the datasets.
* The dependent variables have 589 entries that the stock market movement directionality went down, and 480 entries where the stock market price went up or remained the same.
* One small adjustment has been made to the final datasets, which is known as standardization. This method may help to minimize dataset dissimilarities. Rescaling the features to give them the characteristics of a regular normal distribution is known as standardization (or Z-score normalization) (formula on page 20)


Training, Validation, and Test Set
* dataset for this study has been divided into two parts, 80% for training and 20% for testing the models. 
* Hence, the training data contains 855 observations, and the test data consists of 214 observations.
* Real-world datasets should use a stratified 10-fold cross-validation (Kohavi, 1995). The cross-validation method ensures that the training and test sets include the same proportions of both target groups, which are in this study the upwards and downwards movement of the S&P 500 index price. Cross-validation guarantees the model's validity and reliability; see Section 4.3 for a more comprehensive explanation. The validation set was used as part of a grid search, covered in more detail in Subsection 4.2.3.
* Each of these algorithms was used to create models, and a grid search was applied to find the best model settings, as described in the following subsection. Subsequently, the models were evaluated, and the best performing model for predicting daily S&P 500 movements was selected.
* automated hyperparameter optimization (HPO) has been used in this study. Grid search, also known as full factorial design, is a commonly used HPO tool which automatically finds the best hyperparameters for an algorithm






Doku:
https://janakiev.com/blog/jupyter-virtual-envs/


go to folder
virtualenv venv
.\venv\Scripts\activate
pip install notebook
python -m ipykernel install --name=venv (return: Installed kernelspec venv in C:\ProgramData\jupyter\kernels\venv)
jupter notebook


