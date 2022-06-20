# NPLfoodSpacy

To download the repository on your local computer, write this code in git bash: 

```
git clone https://github.com/JohayraPrithula/NPLfoodSpacy
```

## Installing and Setting up the Libraries

The official page for installation is https://spacy.io/usage. This link provides the necessary commands to execute the installation of the spaCy library. 

## Preparing and Annotating the Data

This repo uses a kaggle dataset to gather food review data, which is the most common contribution to food dataset. The library used can be found in bellow link: https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews

From the review.csv, the summery colomn was chosen and the data was filtered for sentences at least 15 words long to insure a good sentence structure. Importing the filtered sentences in a text file, an online tool was used to annotate the data for food dataset and then exported as a json file. The online tool used is: https://tecoholic.github.io/ner-annotator/

Run the file MakingTheDataset.ipynb to follow the same procedure for any kind of csv data. The final dataset consisted of 324 annotations.

## Implementing spaCy

A basic code for spaCy was implemented using the code from this repo: https://github.com/amrrs/custom-ner-with-spacy3.git . This code will overwrite the existing model and create a model on solely the food dataset. This however makes the model catastropically forget the existing labels and leads to only recognising the food labels in a sentence. 

### Adding the Previous Labels to the Food NER Model

We use add_pipe method which then concats the food dataset ner and the base model ner. This concated file then predicts the other labels apart from food. Details about this method can be found on this video: https://youtu.be/uJ3jWJnADyA

However another problem occured which lead to the model predicting the non-food labels as food labels. To solve this the tok2vec was replaced with the base model's tok2vec. This allows the complete model to accept the new label along with the frozen labels. This repo contains a better look on this method: https://github.com/explosion/projects/tree/v3/tutorials/ner_double

