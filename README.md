# Auto-Vetting

Problem:
  Medical radiology requests, such as x-rays and ultrasound examinations, require vetting in order to determine their urgency (when the scan will be performed) and usefullness (suitible to answer the clinical question).
  The vetting process is time consuming and is subject to intra- and inter-operator variance.
  AI could bring more standardisation to this process and free up time from healthcare professionals.

*First iteration of this project aimed to build a starting model that could differentiate medical requests that specify a date for the examination to be performed "D" and non urgent examinations "C". These two are the most common requests received in ultrasound. Later itterations will aim to differentiate between more vetting option like A (1-2 weeks wait) and B (4 weeks wait) etc. A rubust model will also need to determine if the appropriate examination was requested or if other examinations could be more suitible to asnwer the clinical question*

Model:
  Transfer learning was used with a pretrained model: https://huggingface.co/medicalai/ClinicalBERT | https://www.nature.com/articles/s41591-023-02552-9  which was trained on a large multicenter dataset with a large corpus of 1.2B words of diverse diseases. A large-scale corpus of EHRs from over 3 million patient records were then used to fine tune the base language model.
  The model was adapted for a binary classification task. The final model was trained with ultrasound requests from 106 patients. 54 D (specific date) and 52 C (patients to be scanned within 6 weeks). The validation set had 19 patient requests and the test set had 24. 

  ____________________________________________________________________________________________________________________________________________

A larger dataset of 230 requests was obtained. These are GP requests for upper abdomen ultrasound examinations. The target variable contains 3 classes (0 - 1-2 weeks wait, 1 - 6 weeks wait and 2 - specific date). There are 80 requests for class 0 and 1 and 70 requests for class 2.

Basic NLP (BNLP) was applied. This includes tokenization, lower case, punctuation removal (except <, >, /), term normalisation, spell checking and lemmetizer.

Models tried: BOW + SVC, BOW + RF, BOW + LogReg, BOW + XGBoost , TF-IDF + SVC, TF-IDF + RF, TF-IDF + LogReg, TF-IDF + XGBoost, Bert (ClinicalBERT) and Bert (bert-base-uncased).

Further NLP methods applied when testing the models: BNLP + StopWords, BNLP + negation detection (ND),	BNLP + POS,	BNLP + StopWords (keep negation) + ND,	BNLP + negation + POS,	BNLP + SW + POS,	BNLP + POS + ND + SW.

The best perfoming model was the BOW + LogReg with BNLP + stop word removal. This model achieved an average accuracy of 89%.
