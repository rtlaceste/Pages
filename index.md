## Project 1 - Tweepy API

You can use the [editor on GitHub](https://github.com/rtlaceste/Pages/edit/gh-pages/index.md).

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


![Image](https://raw.githubusercontent.com/rtlaceste/rtlaceste.github.io/gh-pages/WordCloud.JPG)       
*Wordcloud*





![Biden Polarity](https://raw.githubusercontent.com/rtlaceste/rtlaceste.github.io/gh-pages/Biden%20Bar.JPG) 
*Polarity Count*




