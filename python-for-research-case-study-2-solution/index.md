# Python for Research - HarvardX - Case Study 2 Solution

<!--more-->

## Introduction to Problem from HarvardX

> In the six exercises of this case study, we will find and plot the distribution of word frequencies for different translations of Hamlet. Perhaps the distribution of word frequencies of Hamlet depends on the translation -- let's find out!  
For this case study, the functions `count_words_fast` and `word_stats` are defined as in the Case 2 Videos (Videos 3.2.1 through 3.2.6). The code for these functions, which you will need for the following exercises, is given here:  
```Python
import os 
import pandas as pd 
import numpy as np 
from collections import Counter


def count_words_fast(text): 
    text = text.lower() 
    skips = [".", ",", ";", ":", "'", '"', "\n", "!", "?", "(", ")"] 
    for ch in skips: 
        text = text.replace(ch, "") 
    word_counts = Counter(text.split(" ")) 
    return word_counts

def word_stats(word_counts): 
    num_unique = len(word_counts) 
    counts = word_counts.values() 
    return (num_unique, counts)
```

Observe that we have used functions defined in the previous case study which has recorded videos, not the one we have the solutions and also called `Case Study 2: Language Processing`. I highly encourage watching the videos and answering the exercises.

## Exercises

### Exercise 1

> Note that `book_titles` is a nested dictionary, containing book titles within authors within languages, all of which are strings. These books are all stored online, and are accessed throughout this case study. In Exercise 1, we will first read in and store each translation of Hamlet.  
**Instructions**  
Read in the data as a pandas dataframe using `pd.read_csv`. Use the `index_col` argument to set the first column in the csv file as the index for the dataframe. The data can be found at this link within the courseware, and at this link when coming from outside the courseware.  
Complete the following line of code to read in the data:

```Python
hamlets = pd.read_csv("./hamlets.csv", index_col="Unnamed: 0") ## Complete this line of code! ##
hamlets.head()
```

It's good practice to check whether or not our dataframe is correctly initialized. In this code block, we have used `read_csv` to read our .csv file and used `index_col` to select our index column as languages. Our expected output is shown below. Since this case study is much harder than the previous one, I will try to share my results as well as the code.

![First expected output](/images/Python-for-Research-Case-Study-2-Solution/first_output.png)

### Exercise 2

> In Exercise 2, we will summarize the text for a single translation of Hamlet in a pandas dataframe.  
**Instructions**  
Find the dictionary of word frequency in text by calling `count_words_fast()`. Store this as `counted_text`.  
Create a pandas dataframe named data.  
Using `counted_text`, define two columns in data:  
`word`, consisting of each unique word in text.  
`count`, consisting of the number of times each word in word is included in the text.  
Here's the code to get you started:  
How many times does the word Hamlet appear in the text?

```Python
language, text = hamlets.iloc[0]

# Enter your code here.
counted_text = count_words_fast(text)

data = pd.DataFrame(list(counted_text.items()), columns=['word', 'count'])
counted_text["hamlet"]
```

And the expected output is `97`. Here `list(counted_text.items())` gives us a list of tuples of key and value pairs, which we can use to have the rows of our dataframe.

### Exercise 3

> In Exercise 3, we will continue to define summary statistics for a single translation of Hamlet.  
**Instructions** 
Add a column to data named length, defined as the length of each word.  
Add another column named `frequency`, which is defined as follows for each word in data:  
    -If count > 10, frequency is "frequent".  
    -If 1 < count <= 10, frequency is "infrequent".  
    -If count == 1, frequency is "unique".  
How many unique words appear in the text?

Now we are coming to harder parts. From now on,I will try to elaborate more with the methods and variables I have used.

```Python
# write your code here!
def freq(row):
    if row["count"] > 10:
        return "frequent"
    elif 1< row["count"] <=10:
        return "infrequent"
    else:
        return "unique"

data["length"] = data["word"].apply(len)
data["frequency"] = data.apply(freq, axis=1)

len(data[data["frequency"] == "unique"])
```
Expected output is `3348`.

#### What does `apply` do?

Now we need to understand what `apply()` method does. In the official documentation, it says "Apply a function along an axis of the DataFrame.". However, there is one more point waiting to be explained. What is an "axis"? By default, the axis value is equal to 0. This means Pandas will apply the corresponding function (our first input) to each column. If it was equal to 1, it would apply to each row. 

### Exercise 4

> In Exercise 4, we will summarize the statistics in data into a smaller pandas dataframe.  
**Instructions**  
Create a pandas dataframe named `sub_data` including the following columns:  
`language`, which is the language of the text (defined in Exercise 2).  
`frequency`, which is a list containing the strings "frequent", "infrequent", and "unique".  
`mean_word_length`, which is the mean word length of each value in frequency.  
`num_words`, which is the total number of words in each frequency category.  
What is the average word length of the infrequent words?

Here comes the hardest part of this case study for me.

```Python
# write your code here!

languages = ["English", "German", "Portuguese"]
frequencies = ["frequent", "infrequent", "unique"]

data_list = []

for lang in languages:
    for freq in frequencies:
        data_prime = data[data["frequency"] == freq]
        mean_word_length = data_prime["length"].mean()
        num_words = data_prime["count"].sum()
        data_list.append([lang, freq, mean_word_length, num_words])

sub_data = pd.DataFrame(data_list, columns=['language', 'frequency', 'mean_word_length', 'num_words'])

sub_data.loc[sub_data['frequency'] == 'infrequent', 'mean_word_length'].values[0]
```
Expected result is `5.825242718446602`.

Alright, I mostly do not remember how I wrote this part of the code but I will try to elaborate with it. Moreover, in later exercises, HarvardX recommends another approach. I will stick with mine for now. 

Since we need to group by `frequency` -- if you check what we need you can easily see that -- first we create a new dataframe called `data_prime` to store our new dataframe with selected frequency. After that, rest is history. In the last line, we needed to find average word length of the infrequent words and we have found that with using `loc[]` attribute.

### Exercise 5

In the last two exercises, we wrap up what we have covered until now. 

> In Exercise 5, we will join all the data summaries for text Hamlet translation.  
**Instructions**  
The previous code for summarizing a particular translation of Hamlet is consolidated into a single function called `summarize_text`. Create a pandas dataframe grouped_data consisting of the results of `summarize_text` for each translation of Hamlet in hamlets.  
Use a for loop across the row indices of `hamlets` to assign each translation to a new row.  
Obtain the `ith` row of `hamlets` to variables using the `.iloc` method, and assign the output to variables `language` and `text`.  
Call `summarize_text` using language and text, and assign the output to `sub_data`.  
Use the pandas `.append()` function to append pandas dataframes row-wise to `grouped_data`.  
The code below defines `summarize_text`:  
What is the average word length of the frequent words in the German translation?  
How many frequent words are there in the Portugese translation?



```Python
def summarize_text(language, text):
    counted_text = count_words_fast(text)

    data = pd.DataFrame({
        "word": list(counted_text.keys()),
        "count": list(counted_text.values())
    })
    
    data.loc[data["count"] > 10,  "frequency"] = "frequent"
    data.loc[data["count"] <= 10, "frequency"] = "infrequent"
    data.loc[data["count"] == 1,  "frequency"] = "unique"
    
    data["length"] = data["word"].apply(len)
    
    sub_data = pd.DataFrame({
        "language": language,
        "frequency": ["frequent","infrequent","unique"],
        "mean_word_length": data.groupby(by = "frequency")["length"].mean(),
        "num_words": data.groupby(by = "frequency").size()
    })
    
    return(sub_data)
    
# write your code here!
grouped_data = pd.DataFrame()
for idx in range(3):
    language, text = hamlets.iloc[idx]["language"], hamlets.iloc[idx]["text"]
    sub_data = summarize_text(language, text)
    grouped_data = pd.concat([grouped_data, sub_data])

grouped_data
```

Expected output is a dataframe:  
![5th exercise](/images/Python-for-Research-Case-Study-2-Solution/second_output_img.png)

Here you can easily find expected results. Now, let's check how our solution works. First, we have created a dataframe called `grouped_data`. Then, from 0 to 2, we have a loop and we have one-by-one assign `language` and `text` and use these as input while using `summarize_text()`.

Since the last exercise is abnormally easy, I won't be talking about it.
