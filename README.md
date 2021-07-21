# NLP Self Service Comment Classifier (Topic Modeling)

Description: This ML model uses AI on negative NPS comments to categorize the complaints customers have with IPSY. 

NLP self service comment classifier model: predicts comment classes with around 90% accuracy

Significance: This model can be used by the business to better understand customer feedback and comprehend trends in user sentiments (ex. shipping complaints skyrocketed from Feb-Apr). 

Automating the comment labeling process saves the business time, money, and effort, as nobody would have to read through thousands of comments anymore to comprehend what customers are unsatisfied with. 

This model could also help the business determine where to invest in order to improve customer experience, driving a more effective business strategy and potentially avoiding millions in losses and bringing in millions in extra revenue. It would help the business invest in areas that need the greatest improvement, whether it be shipping, personalization, excitement/quality of products, or ensuring that customers receive a variety of products.

Model: Our model uses BERT - Bidirectional Encoder Representations for Transformers (bert-base-uncased) - which is an extremely powerful algorithm developed by Google in 2018. 

BERT was pretrained on BookCorpus - Wikipedia sites (2500M words) and over 11k books (800M words) 

It is able to understand context and enable transfer learning from large corpuses to any NLP task, including topic modeling.

We are using comment embeddings from this pretrained BERT model (bert-base-uncased). We are tokenizing the comments - they are overlaid on the embeddings that were already created in the pretrained model.

How to Train the Model:

To use this model, a user would input the URL link to a csv file in S3, as well as the desired test/train split, number of train epochs, and the path they want to save the model to. The training dataset (csv file) would contain the comments, their respective NPS scores, their labels (personalization, shipping/packaging, repetitive, excitement/quality, value/price, other), as well as other fields. The model will then train on this data and display the results. Once the model is trained, the user would be able to input any csv dataset, and the pretrained model will categorize all of the data for the user and return the results.

How to Use Pretrained Model to Predict Classes:

To use this model, a user would input the URL link to a csv file in S3, as well as the desired test/train split, number of train epochs, and t

Code:

Notebook for training model: https://ipsy-prod.cloud.databricks.com/#notebook/4659645/command/4659655

Notebook for inference using pretrained model: https://ipsy-prod.cloud.databricks.com/#notebook/4676157/command/4676247

Training Pipeline:

For training the model, these are the steps outlined in the notebook:

Step 1: Read labeled data (from user-inputed S3 URL link)

Step 2: Preprocessing (data validation, filtering only important information, adding columns)

Step 3: Flair (filtering out only negative comments)

Step 4: Train Model

Step 5: Save Model

Step 6: Evaluate Model

Inference Pipeline: 

For inference using a pretrained model, these are the steps outlined in the notebook:

Step 1: Read unlabeled data (from user-inputed S3 URL link)

Step 2: Preprocessing (data validation, filtering only important information, adding columns)

Step 3: Flair (filtering out only negative comments)

Step 4: Prediction using pretrained model (link to model user-inputed)

Step 5: Evaluate Results (accuracy, f1 scores), Visualize Findings (confusion matrices)

Email to Lori, Barbara, Sundi, James, Adina, Paula

Send tom morning

replace commas

Model built by Ethan Hsiao (ML intern) and Jyotirmoy Sundi.

