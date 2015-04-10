###About###

`This code is a research/academic project conducted at Kaunas University of Technology (Lithuania) in 2013-05 
by two Informatics faculty MSc students: Aiste Ivonyte & Tomas Uktveris.` 

`Project analyses & applies natural language processing(NLP) algorithms 
to texts extracted from certain year Wikipedia archived news articles.`

The created text analyzer does the following (for a given article):

1. `Extracts named entities (people)` - the named entity recognition (NER) problem [ner.py]
  * uses default Python NLTK ne_chunker + extra logic to detect sex/city/country & remove false positives
2. `Creates a summary from article text` [summarize.py, ph_reduction.py].
Two methods used:
  * Sentences with most frequent words - Summary I 
  * Phrase reduction method - Summary II
3. `Classifies the article into 5 most frequent (top) categories from all analyzed Wikipedia articles` [training.py, training_binary.py]
  * Uses three  NLTK library built-in classifiers - Bayes, MaxEnt (regression) and DecisionTree.<br>Two approaches are used for classifier training:
    * Multiclass - classifier is trained to detect 1 class from multiple (7 classes in total)
    * Binary - trains 3x6 binary classifiers to detect if article represents a given category
4. `Finds people actions` [action.py]
  * Custom token & sentence analysis - reuses NER data to find & assign references.
5. `Resolves references/anaphoras` (named entity normalization - NEN) [references.py]
  * Custom token & sentence analysis - reuses NER data to find required verbs.
6. `Finds people interactions` [interactions.py] 
  * Custom token & sentence analysis - reuses NER & reference data for finding multiple people in sentence and their actions.

###License###
Code & project provided under MIT license (http://opensource.org/licenses/mit-license.php). 
Use at your own risk, no guaranties or warranty included.

Female/male names dictionary used from NLTK project: https://code.google.com/p/nltk/

English words dictionary used from: http://www-01.sil.org/linguistics/wordlists/english/

World cities database used from: http://www.maxmind.com/en/worldcities

###Requirements###
* Python 2.7 (http://www.python.org/download/releases/)
* Python NTLK library (http://nltk.org/) + installed all available corporas (>>> import nltk; nltk.download())

###Directory structure###
``` 
  . - (root directory) contains all source code for the analyzer
  ./archives - contains EN generic word, people names & country dictionaries, SQL city names DB files & scripts
  ./db - contains extracted Wikipedia articles by month
  ./FtpDownloader - Java utility to download articles DB from FTP site
  ./other - misc & example scripts
```
###Usage###

Running the analyzer 
------
* Run article parser & data generation utility to generate the required data files for the next step:
`python data.py`
 
* Run multiclass trainer to generate three types of classifier files:
```
python training.py -b
python training.py -m
python training.py -d
```
* Run binary trainer to generate other classifier files: 
```
python training_binary.py -b
python training_binary.py -m
python training_binary.py -d
```
* Run the main analyzer script to analyze a given article:
```
python main.py -f db/klementavicius-rimvydas/2011-12-03-1.txt
```
###Running other tests###
Some analyzer functionality can be tested separately by running the `test_xxxx.py` files. 

