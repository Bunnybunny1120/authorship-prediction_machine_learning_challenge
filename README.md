
Authorship prediction - Machine Learning Challenge

In this challenge, the task is to predict the lead (first) author of scientific papers based on their metadata. I did this project together with three fellow students, and our group was ranked top 5 at Codalab under the username luizperin: https://codalab.lisn.upsaclay.fr/competitions/8187?secret_key=2116a119-ff89-4e85-85ba-aadd1a0c68ed#results.

Dataset:
The dataset contains two JSON format files:

Training: the metadata, including the lead author of all the papers in the training data.
Testing: the metadata, excluding the lead author, of the papers in the test data.
The loaded data consists of a list of Python dictionaries, with each dictionary corresponding to the record for one paper. The training records specify the lead author (i.e., the first author on the author list) under the key authorID. For the test data, this information is missing, and our task is to predict it. The other features are author name, title, abstract, paperId, venue, and year. Every lead author in the test set occurs at least once in the training data.
Evaluation metric:
The evaluation metric for this task is the accuracy score.

Method
 
* Part of the training data was used as a validation set.
* Submission to Codalab is done after validating results on our validation data.
* We started with a simple baseline approach and only then tried to improve on it.
* Our computational learning experiments, including:
    - feature engineering
    - stratification when splitting data
    - learning algorithm(s)
    - hyperparameter tuning


Feature engineering:
We let target y = df['authorID'], and engineered the feature X = df['abstract'] + ". " + df['title'] + ". " + df['venue'] + ". " + df['year']. The punctuation and one space (". ") are set in between so two strings don't stick to each other when combining. The 'year' integer type is modified into a string for feature concatenation, and the target label 'authorID' is turned into numbers since it was an object. We discovered that there were 5625 different authors in total, whereas 2207 authors appeared only once in the sample, so these one-count authors were filtered out. 

Learning algorithms:
Our very first setup was the CountVectorizer() + Naïve Bayes Multinomial model (MultinomialNB). The accuracy was only 1%. After that, we replaced CountVectorizer with TfidfVectorizer in combination with various models such as Linear Support Vector Classification (LinearSVC), k-nearest neighbors algorithm (K-NN), and Random Forest Classifier. It turned out that MultinomialNB outperformed other algorithms.

Hyperparameter tuning:
In the CountVectorizer, we tried stop_words = 'english' + the MultinomialNB model, which enabled the accuracy to rise from 1% to 3%. The TfidfVectorizer, helped us eliminate the words that appeared frequently in all samples by giving them very little or no weight. Three hyperparameters are tuned: min_df = 0.0002, max_df = 0.8, and ngram_range = (1,2). This way, we can eliminate the features that appeared only 0.02% of the time and the words that appeared in 80% of the whole document. Regarding the ngram_range, the unigram and bigrams gave the most desirable outcome. We have tried trigrams, but it did not give us a significant improvement. Moreover, the max_features was initially one of the hyperparameters we used. A max_features = 160,000 was used, but it was too heavy to run, so it was tuned into 100,000. Based on this setting, the hyperparameter alpha for the MultinomialNB algorithm was adjusted to 0.00025.

Findings and conclusion:
Our aim is to make predictions and do better than the baseline of 15% accuracy. We started with a simple untuned model with 1% accuracy. After a few breakthrough actions: feature selection, data cleaning, stratification, the usage of TfidfVectorizer, and hyperparameter tuning, we have significantly increased the accuracy rate up to 21.05% at validation. However, the accuracy was only 15.83% at the first submission using test set at Codalab, indicating overfitting. This was fixed by including samples with authors who appeared only once (about 39%). After training the model again with the whole training set, our prediction reached a desirable accuracy, consistent with our validation.

While we adopted a simple approach, other methods like utilising BERT model could be explored for better performance. A 90% accuracy rate is desirable, but real-life scenarios are chaotic and unpredictable. A model is a tool, and its value lies in fulfilling its intended purposes effectively and ethically. Prioritizing interpretability and fairness may outweigh raw accuracy in some applications. Continuous learning and adaptation are essential to address challenges and build reliable AI systems for societal advancement.
## Demo

Insert gif or link to demo


## Documentation

[Documentation](https://linktodocumentation)


## Contributing

Contributions are always welcome!

See `contributing.md` for ways to get started.

Please adhere to this project's `code of conduct`.

## Color Reference

| Color             | Hex                                                                |
| ----------------- | ------------------------------------------------------------------ |
| Example Color | ![#0a192f](https://via.placeholder.com/10/0a192f?text=+) #0a192f |
| Example Color | ![#f8f8f8](https://via.placeholder.com/10/f8f8f8?text=+) #f8f8f8 |
| Example Color | ![#00b48a](https://via.placeholder.com/10/00b48a?text=+) #00b48a |
| Example Color | ![#00d1a0](https://via.placeholder.com/10/00b48a?text=+) #00d1a0 |


## Badges

Add badges from somewhere like: [shields.io](https://shields.io/)

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
[![GPLv3 License](https://img.shields.io/badge/License-GPL%20v3-yellow.svg)](https://opensource.org/licenses/)
[![AGPL License](https://img.shields.io/badge/license-AGPL-blue.svg)](http://www.gnu.org/licenses/agpl-3.0)


## Deployment

To deploy this project run

```bash
  npm run deploy
```


## Authors

- [@octokatherine](https://www.github.com/octokatherine)

