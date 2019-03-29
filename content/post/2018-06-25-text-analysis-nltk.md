---
title: "Text Analysis-Python"
date: "2018-06-25T21:49:57-07:00"
categories:
  - Products
tags:
  - Python
  - Text analysis
  - Data
---

This is a brief introduction to text analysis by using python. To be general, the processes are as follows:

1. Set up correct working directory for importing document to process.
2. Import .txt files in Python.
3. Work towards the clean dataset as needed.
4. Visualize data as requested.

There are many different ways to clean the dataset and alternate algorithms for text analysis. The following is the code along with some explaination of what I have learned for processing texts.

Here, I have used the County Zoning Regulation as a sample text file to work with.
```r
import os
import nltk

# First create a filepath to point to where we want the file to go.

relativepath = os.path.join('..', '..', 'data','Corpus')
filepath = os.path.join(relativepath, 'CountyZoneReg.txt')

# Then use the 'with' command to open the file in WRITE mode (hence 'w')

with open(filepath, 'r') as f:
    narrative_string = f.read()
```

```r
print(narrative_string)
```
By print, we can check if we have imported the doc correctly:

```r
 ZONING
       REGULATIONS




FIRST ADOPTED BY THE BOARD OF COUNTY COMMISSIONER, SEPTEMBER 23, 1966

             Chapter XII, Article 3 of the Douglas County Code
    Incorporated into the Douglas County Code by Resolution No. 09-11

    Amendments:      Resolution 13-02 Agritourism
                     Resolution 13-03 Special Events
                     Resolution 14-12 Revisions to Agritourism

                  CONTAINING ALL AMENDMENTS THROUGH
                           April 16, 2014

                      OFFICIAL COPY

                                 Page v
Chapter XII – Douglas County Zoning Regulations                                         Article 3
                                       TABLE OF CONTENTS
                                       .
                                       .
                                       .

```


Method 1: we iterate through our list of punctuation markers,
and use the replace() method to replace the marker with nothing.Note that we have to be selective about which punctuation we want to remove. For instance, the '--' must be removed by itself, while we have an opion to remove apostrophes (as in possessives or contractions).

```r
def remove_punc(text):
    text = text.replace('--', ' ')
    #punctuation = '!@#$%^&*()_-+={}[]:;"\'|<>,.?/~`'
    punctuation = '!@#$%^&*()_-+={}[]:;"|<>,.?/~`'
    for marker in punctuation:                     #marker here can be replaced by anything
        print(marker)
        text = text.replace(marker, "")            #if here the marker will be the same word
    return text


# you can play around, inputting different strings here, to see what the function will strip.
short_text = "12-316-2.03.      The parking requirements in this section do not limit special requirements which may be imposed in connection with Conditional Uses (section 12-319) or Special Use Exceptions (section 12-323-3)."
print(remove_punc(short_text))
```

Method 2: We iterate through the text itself, and if the character
is not a punctuation mark, then we add it to the 'clean_text' string.
Again, we have to remove the '--' character by itself.


```r
def remove_punc2(text):
    text = text.replace('--', ' ')
    #punctuation = '!@#$%^&*()_-+={}[]:;"\'|<>,.?/~`'
    punctuation = '!@#$%^&*()_-+={}[]:;"|<>,.?/~`'
    clean_text = ""
    for character in text:
        if character not in punctuation:
            clean_text += character
    return clean_text

short_text2 = "Section 309B       ‘R-T’ RURAL-TOURISM BUSINESS DISTRICT REGULATIONS"
print(remove_punc2(short_text2))
```
The "-" is removed.
```r
Section 309B       ‘RT’ RURALTOURISM BUSINESS DISTRICT REGULATIONS
```

Method 3. we use regular expressions.

```r
import re

def remove_punc3(text):
    text = text.replace('--', ' ')
    text = re.sub(r'[^\w\s]','', text)
    return(text)

short_text3 = "12-316-2.03.      The parking requirements in this section do not limit special requirements which may be imposed in connection with Conditional Uses (section 12-319) or Special Use Exceptions (section 12-323-3)."
print(remove_punc3(short_text3))
```

```r
12316203      The parking requirements in this section do not limit special requirements which may be imposed in connection with Conditional Uses section 12319 or Special Use Exceptions section 123233
```

Remove punc:
```r
narrative_string_nopunct = remove_punc(narrative_string)
print(narrative_string_nopunct)

```

```r
# Lowercase the whole Narrative string.

clean_narrative_string = narrative_string_nopunct.lower()

# Tokenize!

import nltk
narrative_tokens = nltk.word_tokenize(clean_narrative_string)
print(narrative_tokens[:25])
```

```r
['zoning', 'regulations', 'first', 'adopted', 'by', 'the', 'board', 'of', 'county', 'commissioner', 'september', '23', '1966', 'chapter', 'xii', 'article', '3', 'of', 'the', 'douglas', 'county', 'code', 'incorporated', 'into', 'the']
```

# Frequencies
Now that we've had a first pass at word tokenization (keeping only word tokens), let's look at counting word frequencies. Essentially we want to go through the tokens and tally the number of times each one appears. Not surprisingly, the NLTK has a very convenient method for doing just this, which we can see in this small sample (the first 50 word tokens):

```r
narrative_tokens_sample = narrative_tokens[:50]
sample_freqs = nltk.FreqDist(narrative_tokens_sample)
sample_freqs
```

```r
FreqDist({'adopted': 1,
          'agritourism': 2,
          'all': 1,
          'amendments': 2,
          'april': 1,
          'article': 1,
          'board': 1,
          'by': 2,
          'chapter': 1,
          'code': 2,
          'commissioner': 1,
          'containing': 1,
          'county': 3,
          'douglas': 2,
          'events': 1,
          'first': 1,
          'incorporated': 1,
          'into': 1,
          'no': 1,
          'of': 2,
          'regulations': 1,
          'resolution': 4,
          'revisions': 1,
          'september': 1,
          'special': 1,
          'the': 3,
          'through': 1,
          'to': 1,
          'xii': 1,
          'zoning': 1})
```

This FreqDist object is a kind of dictionary, where each word is paired with its frequency (separated by a colon), and each pair is separated by a comma. This kind of dictionary also has a very convenient way of displaying results as a table:

```r
sample_freqs.tabulate(10)
```

```r
 resolution         the      county          by          of     douglas        code  amendments agritourism      zoning 
          4           3           3           2           2           2           2           2           2           1 

```
Now let's do it again with the whole text of Douglass's CountyZoneReg:


```r
narrative_freqs = nltk.FreqDist(narrative_tokens)
narrative_freqs.tabulate(10)
```

```r
the    of   and    or     a    to    in    be shall   for 
 3557  2419  1686  1650  1270  1049   898   871   804   698 
```

More cleanups:
There are several other things we might want to 'clean' out of this file. Depending on our goals, we may want to:

* Remove numbers
* Remove common words (called stopwords)
* Remove textual markers (e.g., 'page 1 of 132')


According to different needs, more cleanning work or visualizing package will be applied such as the Pandas.


