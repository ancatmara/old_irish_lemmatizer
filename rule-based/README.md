# Early Irish Lemmatizer

A lexicon-based lemmatizer for Early Irish showing the average accuracy of 65,71 % (known + unknown words). 

## Usage

### From command line
The lemmatizer takes two positional arguments: input type and input itself. For type, choose one of the following:
* S is for standard input. In this case, the next argument will be regarded as an input text, lemmatized and printed to the command line.
* F is for files/folders. In this case, the next argument will be regarded as a path to an input file/folder. This file/the files in this folder will be lemmatized, and the results will be saved in (a) separate file(s).

Lemmatizing a word or phrase:
```
python lemmatizer.py S "Is acher in gaíth in-nocht, fu-fúasna fairggae findfholt"
is aicher in gáeth innocht fo-fúasna fairrge findfholt
```

Lemmatizing a file:
```
python lemmatizer.py F input.txt
```

Lemmatizing files in a folder:
```
python lemmatizer.py F input_files
```


### As a Python library

**Lemmatize a text**

*Lemmatizes the text from a file and writes the output into another file; returns a dictionary with unknown forms and their counts*

```python
from lemmatizer import *
nondict = Lemmatizer.process_text(path)
```

**Lemmatize all texts in the directory**

*Lemmatizes the text from all txt files in the directory and writes the output into separate files; returns a dictionary with unknown forms and their counts*

```python
nondict = Lemmatizer.process_files(path)
```

**Lemmatize a string**

*Initializes the Lemmatizer class for a string*

There are two available methods for now, 'baseline' and 'predict'. 'Baseline' returns lemmas for all known words
and demutated forms for unknown words; 'predict' predicts lemmas for unknown words. The default method is 'predict'.

```python
lem = Lemmatizer(string, method='baseline')
lemmatizedString = lem.lemmaText
```

It has the following attributes:
* `lem.text` – input string cleaned from punctuation and non-word symbols
* `lem.words` – list of tokens
* `lem.lemmaText` – lemmatized string 
* `lem.nondict` – list of unknown words
* `lem.recall` – shows the percentage of known forms in the string
* `lem.nr_tokens` – number of tokens in a string
* `lem.nr_unique` – number of unique tokens in a string

**Demutate a word**

*Returns a demutated word*
```python
demutatedWord = Lemmatizer.demutate(word)
```

**Predict lemmas for unknown forms**

*Takes a dictionary of OOV-words and their counts as input and creates two files for further manual revision:
OOV-words sorted by frequency higher than a given threshold (the  default one is 0) and a file with triplets of OOV-word, closest known form from the dictionary and proposed lemma. 
Returns a list of tuples.*

```python
proposed = Lemmatizer.predict_lemmas(file_for_proposed, file_for_nondict, nondict, threshold=5)
```

**Update a dictionary**

*Adds words from a preformatted file ("lemma\tform1,form2...\n") to the "forms.json" dictionary and also updates dictionaries of form and lemma probabilities*

```python
Lemmatizer.update_dict(path_to_dict, path_to_update)
```


## Evaluation

There is a test set of 50 random sentences (50\_gold\_test.txt) and a manually lemmatized 




(50\_gold\_lem.txt) available for evaluation.
