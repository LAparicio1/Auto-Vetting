# Auto-Vetting

Problem:
  Medical radiology requests such as x-rays and ultrasound examinations require vetting in order to determine their urgency (when the scan will be performed) and usefullness (suitible to answer the clinical question).
  The vetting process is time consuming and is subject to intra- and inter-operator variance.
  AI could bring more standardisation to this process and free up time from healthcare professionals.

*First iteration of this project aimed to build a starting model that could differentiate medical requests that specify a date for the examination to be performed "D" and non urgent examinations "C". These two are the most common requests received in ultrasound. Later itterations will aim to differentiate between more vetting option like A (1-2 weeks wait) and B (4 weeks wait) etc. *

Model:
  Transfer learning was used with a pretrained model: https://huggingface.co/medicalai/ClinicalBERT | https://www.nature.com/articles/s41591-023-02552-9  which was trained on a large multicenter dataset with a large corpus of 1.2B words of diverse diseases. A large-scale corpus of EHRs from over 3 million patient records were then used to fine tune the base language model.
  The model was adapted for a binary classification task. The final model was trained with ultrasound requests from 106 patients. 54 D (specific date) and 52 C (patients to be scanned within 6 weeks). The validation set had 19 patient requests and the test set had 24. 
