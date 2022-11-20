## Table of Contents
* [Overview](#overview)
* [Purpose](#purpose)
* [Labelling](#labelling)
* [BERT](#bert)
* [Analysis](#analysis)
* [Transfer Learning](#transfer-learning)
* [Measurement and Metrics](#metrics)
* [Datasets](#datasets)

## Overview  
The timing of this text summarization project coincides with a special era in Natural Language Processing (NLP), during sudden and enormous gains in model architecture and performance, and in particular, within Transfer Learning methods utilizing recently released models pretrained on enormous corpora (e.g., entire Wikipedia, Reddit, Book Corpus, more). As a result, new SOTA benchmarks are breaking old ones by incredible margins, sometimes on a weekly basis, and each new model hopes to top the metric charts. As NLP researcher Sebastian Ruder notes:  
That is, just a couple of years ago, practitioners in Computer Vision experienced the beginning of a similar leap in model performance while NLP progress remained stagnant in comparison. But much has changed. 

## Purpose  
This project has a two-fold aim:  
- First, to produce two summarization models in order to study the relationship between word and sentence probabilities, token prediction methods, contextual proximity vs semantic inter-sentence coherence, and syntactic representation.  In particular, this project's focus centers on modeling with an emphasis on powerful pretrained networks which for the first time allows NLP to apply and to encourage the use of transfer learning methods. More on these considerations follow later in this document.  
- Second, through an analysis of extractive summarization algorithms to provide informed research within the context of the current state of NLP in its present and dramatic transformation occurring at breakneck speed on a weekly--and sometimes--daily basis.

## BERT
The [paper's](https://arxiv.org/abs/1810.04805) authors state:

 > "BERT outperforms previous methods because it is the first *unsupervised, deeply bidirectional* system for pre-training NLP."

BERT considers context as part of its inherent design. Not only is BERT an unsupervised model, it also is a transformer model. No convolutions. No recurrent movement. Its bidirectional capability allows it to consider tokens from both the left *and* right side--on all layers of the net. In other words, it surpasses earlier models capable only of predicting context from one-sided input or "shallow bidirectional" input. In addition, BERT masks (drops) 15 percent of its tokens and predicts on those, further pushing to model relationships among tokens and creating a sophisticated framework for generating probabilities and text output.

On top of my BERT-Large model, utilizing K-Means as a way of graphing relationships and most importantly, measuring cluster proximity via edge weights to determine token similarity. The model also borrows from OpenAI's tokenizer which I learned really is not necessary as BERT's own SentencePiece tokenizer is impressive in its own right.  

Although much is made of BERT's ingesting of enormous corpora, additional training using domain-specific data helps performance as is the case with most pretrained models. I chose from the limited array of standardized NLP summarization datasets. Given the extensive resources necessary to train BERT, not to mention hyperparameter tuning, the BBC News dataset was reasonable in size and includes both full-text articles and accompanying gold summaries. In addition, as you'll read below--if you can summon the patience--my impetus for this project is far less about posting a nice ROUGE or BLEU score which in general is relatively easy to do with pretrained transformer models. Nor am I holding my breath to measure the difference between state-of-the-art architecture and well, one that doesn't learn. You might characterize this difference as morphological even if the words they both produce are not. Instead, my concerns are more closely tied to semantic, syntactic, inter-sentence coherence--human-readability, contextual sophistication--within news text or otherwise. Hence the title.

## Analysis  
For the purposes of demonstration, we'll use summarized examples of a full-text passage passed in from a URL: the Wikipedia page for the critically-acclaimed HBO series, Chernobyl.  
*Full text is excluded here for space and length considerations. However, I've included those files in the repo's [full_text](https://github.com/dhk3136/bert-vs-vanilla-summarization/tree/master/full_text) directory.*
BERT intentionally masks a small ratio of words so that it can predict probabilities of the correct word--in context. Part of this masking includes subwords (e.g., I ##ay t## nis) made by BERT's sentence piece tokenizer. This is different from measuring distance or weighted connections as a metric of semantic similarity. In addition, BERT is ambidextrous (maybe too much on the anthropomorphism). The model can take input from both sides of *all layers* which expands its contextual framework resulting in a huge advantage over unidirectional input. 
The baseline model's results were somewhat extreme in the sense that it provided both useful and extraneous details. While the first and third sentences are eloquent in their description. The second sentence provides a bit of useful information, letting us know who's playing the lead. While this knowledge should not be discarded, its positioning as a top-n sentence is curious. The last sentence provides us with a good piece of trivia, but if you refer to the full text, you'll see that the sentence is a rebuttal to misconceptions about the usage of those plastic screens. Yet, the summary is readable. So, with regard to inter-sentence coherence, what's the problem? Well, there's one glaring mistake the vanilla model could not detect: it never mentions the name of the miniseries. The word Chernobyl appears along with some context, but ultimately, the summary leaves the reader to infer its precise topic.  

## Transfer Learning
Here's how I consider transfer learning in general:  

> *TRANSFER LEARNING = PRETRAINING + DOMAIN KNOWLEDGE - (TIME COMPRESSION + MATERIAL RESOURCE)*

## Measurement and Metrics: Pros and Cons
### Ambiguous tasks make labeling hard

## Datasets  
 - [CNN/DailyMail](https://github.com/abisee/cnn-dailymail): A very common dataset for NLP summarization. Includes both full text articles and their accompanying reference (gold) summaries. This is a large dataset. Instructions for loading preprocessed data or DIY options are available.
 - [Webis-TLDR-17 Corpus](https://zenodo.org/record/1168855): A more recent and very interesting large dataset. It was created by mining self-written summaries on Reddit marked by users' comments who appended posts with a literal TL;DR.
 - [Gigaword](https://www.ldc.upenn.edu/language-resources): Another common dataset for summarization in part because it constitutes one of the largest of the corpora. Plus, there are multiple editions. But--and it's a big but (sorry)--you've got to pay for it, and it's not cheap. Because it's so widely used, I'd wager there are copies of the dataset floating around the web, but as usual it's on you to read the fine print.
 - [Opinosis](https://github.com/kavgan/opinosis/blob/master/OpinosisDataset1.0_0.zip): A useful dataset for summarization of reviews and complete with gold summaries. A smaller dataset, it's best for those who don't have a ton of compute to spare. It's organized around topics (e.g., "performance of Toyota Camry") and the reviews within those topics. It was released alongside a summarization model, so you might also want to check that out. Link goes directly to a zip file.
 - [WikiHow](https://github.com/mahnazkoupaee/WikiHow-Dataset): The dataset author explains it best: "Each article consists of multiple paragraphs and each paragraph starts with a sentence summarizing it. By merging the paragraphs to form the article and the paragraph outlines to form the summary, the resulting version of the dataset contains more than 200,000 long-sequence pairs." This is considered one of the largest datasets for summarization. I found the setup to be somewhat awkward/confounding, but after that you're good to go.
 - [BBC News](https://www.kaggle.com/pariza/bbc-news-summary): I've included this dataset in the `data` directory. It's a smaller, lightweight but complete dataset of news articles--and reference summaries for each article. Not bad.
 - Other:  
  - [Kaggle](https://www.kaggle.com) is always a good place to look. I've tried their [New York Times](https://www.kaggle.com/nzalake52/new-york-times-articles) article dataset and where I found the BBC News dataset.  
  - While the NYT dataset doesn't come with gold summaries, it's fairly common to use a news dataset to predict the headline of an article (especially when gold summaries are unavailable).  
  - Also, you might find it worthwhile to visit the relatively new [TensorFlow Datasets](https://www.tensorflow.org/datasets) site. I've only skimmed their offerings, but I do know they have the CNN/DailyMail dataset (with additional options) among others. The real benefit is that they provide very easy code to import any of their datasets through a `tfds.load()` helper function. For example, this could be a more efficient way to load in the CNN/DailyMail dataset. Give it a try!
  - Lastly, the [NLP Progress](http://nlpprogress.com/english/summarization.html) Summarization section and [Papers with Code](https://www.paperswithcode.com) are great resources to see which datasets and high-performance models are currently utilized by SOTA competitors. Fair warning, Papers with Code encompasses all of deep learning--not just NLP, so it's super easy to get distracted there with so many novel ideas.