## Project 1 - Decision Trees/Random Forest Classifier



Using Python's Machine Learning library - sci-kit learn, I created a model to detect the presence of Kyphosis based on data of actual Kyphosis patients.

### Exploring Data
Utilizing Python's Seaborn library to visualize and explore the data.


![Image](https://raw.githubusercontent.com/rtlaceste/rtlaceste.github.io/main/kyphosis.JPG)       
*Seaborn Pairplot*


```python

from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import classification_report,confusion_matrix
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score


X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33)

dtree = DecisionTreeClassifier()
dtree.fit(X_train, y_train)
predictions = dtree.predict(X_test)


rfc = RandomForestClassifier(n_estimators=200)
rfc.fit(X_train,y_train)
rfc_pred = rfc.predict(X_test)


accuracy_score(y_test, rfc_pred)


```





### Conclusion

The Decision Trees Classifier had 81% accuracy while the Random Forest Classifier had 77% accuracy in accurately identifying the presence of Kyphosis

## Project 2 - Natural Language Processing

Using Python's nltk and sklearn libraries, I created two pipelines to classify if a message was SPAM (auto-generated) or HAM (human-generated). I also used two different classifiers (Naive Bayes and Random Forest Classifier) to observe which pipeline would perform better.


```python

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import string
from nltk.corpus import stopwords
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.feature_extraction.text import TfidfTransformer
from sklearn.naive_bayes import MultinomialNB
from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline
from sklearn.ensemble import RandomForestClassifier


def text_process(mess):
    """
    1. Remove punctuation and stop words
    2. Return list of clean text words
    """
    
    nopunc = [char for char in mess if char not in string.punctuation]
    
    nopunc = ''.join(nopunc)
    
    return [word for word in nopunc.split() if word.lower() not in stopwords.words('english')]


bow_transformer = CountVectorizer(analyzer=text_process).fit(messages['message'])
messages_bow = bow_transformer.transform(messages['message'])
tfid_transformer = TfidfTransformer().fit(messages_bow)
tfidf4 = tfid_transformer.transform(bow4)
messages_tfidf = tfid_transformer.transform(messages_bow)
all_pred = spam_detect_model.predict(messages_tfidf)


pipeline = Pipeline([
    ('bow',CountVectorizer(analyzer=text_process)),('tfidf',TfidfTransformer()),('classifier', MultinomialNB())
])

pipeline2 = Pipeline([
    ('bow',CountVectorizer(analyzer=text_process)),('tfidf',TfidfTransformer()),('classifier', RandomForestClassifier())
])


pipeline.fit(msg_train,label_train)

predictions = pipeline.predict(msg_test)
pipeline2.fit(msg_train,label_train)
predictions2 = pipeline2.predict(msg_test)

```
*NLP Models*


![Models](https://raw.githubusercontent.com/rtlaceste/rtlaceste.github.io/main/NLP2.JPG)

*Pandas Dataframe of messages and classification*

### Conclusion
I found that Naive Bayes had a total accuracy of 97%, while the Random Forest Classifier also had an accuracy of 97%.





## Project 3 - Tweepy API


One fun idea I had one day was to analyze the tweets of Joe Biden to see if an algorithm would be able to guess if his tweets carried a positive, negative, or neutral tone.

### Preprocessing

Regex was used to remove @ mentions as well as links, as these type of strings were not needed for the analysis.

```python

def cleanTxt(text):
    text = re.sub(r'@[A-Za-z0-9]+', "", text) #Removes @mentions
    text = re.sub(r"#", '', text)
    text = re.sub(r"RT[\s]+", '', text)
    text = re.sub(r"https?:\/\/\S+", "", text)
    
    return text

def getSubjectivity(text):
    return TextBlob(text).sentiment.subjectivity

def getPolarity(text):
    return TextBlob(text).sentiment.polarity

df['Subjectivity'] = df["Tweets"].apply(getSubjectivity)
df['Polarity'] = df["Tweets"].apply(getPolarity)

```


![Image](https://raw.githubusercontent.com/rtlaceste/rtlaceste.github.io/gh-pages/WordCloud.JPG)       
*Wordcloud*





![Biden Polarity](https://raw.githubusercontent.com/rtlaceste/rtlaceste.github.io/gh-pages/Biden%20Bar.JPG) 

*Polarity Count*




### Conclusion

90/100 of Biden's last 100 tweets carried either a negative or neutral tone, while the rest had a negative tone. 


## Project 4 - Visualizing Data + SQL scripting

In this project, Tableau Public was used for data visualization and MySQL for the sql server.

### MySQL

Logging into SQL as well as inserting a table and values.


```python

import mysql.connector
from mysql.connector import Error
from mysql.connector import errorcode

try:
    connection = mysql.connector.connect(host='localhost',
                                         database='**',
                                         user='**',
                                         password='**')
    mySql_insert_query = f"""INSERT INTO Crime (Id, Date, City, District) 
                           VALUES 
                           {data} """

    cursor = connection.cursor()
    cursor.execute(mySql_insert_query)
    connection.commit()
    print(cursor.rowcount, "Records inserted successfully")
    cursor.close()

```


![Image](https://raw.githubusercontent.com/rtlaceste/rtlaceste.github.io/gh-pages/Tableau.JPG)       
*Tableau Dashboard*

## Project 5 - Flask Application

In this project I used Flask to set up a website's server side. The website can be found [here](https://rtlaceste.pythonanywhere.com/).


```python

from flask import Flask, render_template, url_for, request, redirect
import csv

app = Flask(__name__)
print(__name__)


@app.route('/')
def my_home():
    return render_template('index.html')


@app.route('/<string:page_name>')
def html_page(page_name):
    return render_template(page_name)


def write_to_file(data):
    with open('database.txt', mode='a') as database:
        email = data["email"]
        subject = data["subject"]
        message = data["message"]
        file = database.write(f'\n{email},{subject},{message}')


def write_to_csv(data):
    with open('database.csv', mode='a', newline='') as database2:
        email = data["email"]
        subject = data["subject"]
        message = data["message"]
        csv_writer = csv.writer(database2, delimiter=',', quotechar='"', quoting=csv.QUOTE_MINIMAL)
        csv_writer.writerow([email, subject, message])


@app.route('/submit_form', methods=['POST', 'GET'])
def submit_form():
    if request.method == 'POST':
        try:
            data = request.form.to_dict()
            write_to_csv(data)
            return redirect('/thank_you.html')
        except:
            return 'did not save to database'
    else:
        return 'Something went wrong, please try again'
```

![Image](https://raw.githubusercontent.com/rtlaceste/rtlaceste.github.io/main/flask.JPG)       
*Website Interface*















