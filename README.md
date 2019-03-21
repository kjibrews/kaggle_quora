# Kaggle Quora Insincere Questions
This repo contains my approach to [Kaggle Insincere Questions Classification](https://www.kaggle.com/c/quora-insincere-questions-classification).

**Description:**    
  Quora is an online question and answer platform with content created from its community of users. To enable a safe community and uphod their policy of "Be Nice, Be Respectful", Quora needs to eliminate "insincere" questions -- those founded upon false premises, or that intend to make a statement rather than look for helpful answers, on their platform. These types of questions include questions that are: disparaging or inflammatory, asked purely for shock value, have a non-neutral tone and are not grounded in reality.

* **Examples of Sincere questions:**
  * How did Quebec nationalists see their province as a nation in the 1960s?  
  * Do you have an adopted dog, how would you encourage people to adopt and not shop?
* **Examples of Insincere questions:**
  * Which babies are more sweeter to their parents? Dark skin babiesor light skin babies?  
  * If blacks support school choice and mandatory sentencing for criminals why don't they vote Republican?  

The aim of this competition is to develop models that identify and flag insincere questions. 

* **Limitations of competition:**
  * Kernels only competition
    * No custom packages
    * RAM Limitations 
    * RAM limitations  (CPU : 17 GB, GPU: 14 GB), 
    * if using GPU no custom packages were allowed 
    * Runtime limitations (CPU: 6 hours, GPU: 2 hours)
  * Data needed to be cleaned before being processed by the model.
  * Class Imbalance in training set (Sincere: ~95% , Insincere ~5%). 
  * English only word embeddings
    * Quite a few non- English expressions

## Data
Data fields:
* qid - unique question identifier
* question_text - Quora question text
* target - a question labeled "insincere" has a value of 1, otherwise 0

## File descriptions:
* train.csv - the training set  
    - The training data includes the question that was asked, and whether it was identified as insincere (target = 1).
    - The ground-truth labels contain some amount of noise: they are not guaranteed to be perfect. 
    - It was noted also that the distribution of questions in the dataset should not be taken to be representative of the distribution 
    of questions asked on Quora. This is, in part, because of the combination of sampling procedures and sanitization measures that have
    been applied to the final dataset.
* test.csv - the test set
* sample_submission.csv - A sample submission in the correct format
* embeddings   
   External data sources are not allowed for this competition.Four word embeddings were provided that can be used in models.
  * [GoogleNews-vectors-negative300](https://code.google.com/archive/p/word2vec/)
  * [glove.840B.300d](https://nlp.stanford.edu/projects/glove/)
  * [paragram_300_sl999](https://cogcomp.org/page/resource_view/106)
  * [wiki-news-300d-1M](https://fasttext.cc/docs/en/english-vectors.html)


## Initial Approach
### Data Cleaning
Lowercasing
Replacement using self defined dictionaries to map replacements
  * Contractions,
  * Unknown characters
  * Commonly misspelled word
  * Lemmatisation
Punctuation removal
Removal of common and rare words

### Data Processing
GLOVE, WikiFastText and Paragram English word embeddings were used to map words to a dense vector space. 

### Model Testing
Try a variety ofNeural Net models, Logistic Regression and ADA Boost with abnd without the word embeddings.

### Model Selection
Based on performance and score select a final model.

*To do:* 
- [] Try back propogation for unknown characters

## Result
Scoring is evaluated usin the  [F1 Score](https://en.wikipedia.org/wiki/F1_score) between the predicted and the observed targets.
