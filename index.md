## Project 1 - Twitter Scraping Analysis

You can use the [editor on GitHub](https://github.com/rtlaceste/Pages/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

One fun idea I had one day was to analyze the tweets of the president-elect to see if an algorithm would be able to guess if his tweets carried a positive, negative, or neutral connotation. 

### Markdown

Cleaning up the data

```python
Syntax highlighted code block

def cleanTxt(text):
    text = re.sub(r'@[A-Za-z0-9]+', "", text) #Removes @mentions
    text = re.sub(r"#", '', text)
    text = re.sub(r"RT[\s]+", '', text)
    text = re.sub(r"https?:\/\/\S+", "", text)
    
    return text
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/rtlaceste/Pages/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
