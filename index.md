## Project 1 - Twitter Sentiment Analysis

You can use the [editor on GitHub](https://github.com/rtlaceste/Pages/edit/gh-pages/index.md).

One fun idea I had one day was to analyze the tweets of Joe Biden to see if an algorithm would be able to guess if his tweets carried a positive, negative, or neutral tone.

### Markdown

Cleaning up the data

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





For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/rtlaceste/Pages/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
