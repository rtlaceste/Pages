## Project 1 - Tweepy API

[editor on GitHub](https://github.com/rtlaceste/Pages/edit/gh-pages/index.md).

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


## Project 2 - Visualizing Data + SQL scripting

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

## Project 3 - Flask

In this project I used Flask to set up a website's server side system. The website can be found [here](https://rtlaceste.pythonanywhere.com/).


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















