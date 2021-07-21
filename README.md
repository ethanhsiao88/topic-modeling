# NLP Self Service Comment Classifier (Topic Modeling)

## Description: The ML model categorizes negative NPS comments based on customers' complaints 

- NLP self service comment classifier model: predicts comment classes with around 90% accuracy <br />




## Significance: This model can be used by the business to better understand customer feedback and comprehend trends in user sentiments (ex. shipping complaints skyrocketed from Feb-Apr) 

- Automating the comment labeling process saves the business time, money, and effort. Now, no human has to read through thousands of comments anymore to comprehend what can be improved

- This model helps the business determine where to invest in order to improve customer experience, driving a more effective business strategy and potentially bringing in millions in extra revenue

- It would help the business invest in areas that need the greatest improvement, whether it be variety, shipping, personalization, or excitement/quality of products




Model: Our model uses BERT (Bidirectional Encoder Representations for Transformers) 

- BERT was pretrained on BookCorpus: Wikipedia sites (2500M words) & over 11k books (800M words) 

- An extremely powerful algorithm developed by Google in 2018 - able to understand context and enable transfer learning from large corpuses to any NLP task, including topic modeling

- We're using comment embeddings from a pretrained BERT model (bert-base-uncased). We're tokenizing the comments - they're overlaid on the embeddings already created in pretrained model




How to Train the Model:

- To train this model, a user must input the URL link to a training dataset in S3

 - Training dataset must be in csv format

 - Training dataset must contain the following columns (syntax must be identical):

Start Date

End Date

How likely are you to recommend the Glam Bag to a friend?

What is the most important reason for your recommendation answer?

topic_type

Recommended labels: personalization, shipping/packaging, repetitive, excitement/quality, value/price, other (syntax should be identical)

userId

NOTE: Since this is a csv, it is parsed by commas. To avoid errors, replace all commas with spaces

The user can also adjust 3 other fields:

Desired test/train split (default = 0.2; can change to 0.1, 0.15, 0.25, or 0.3)

Number of train epochs (default = 15; can change to 5, 10, or 20)

Path they want to save the model to (default = dbfs:/mnt/ipsy-databricks-mlp/research/ethan/monolabeled-model-full-w-others-copy)

Click “Run All” and watch the model train! 

Evaluation of the model will also be displayed. Metrics include the model’s accuracy, weighted f1 score, f1 scores for each label, as well as confusion matrices and normalized confusion matrices

Results from model trained on over 10,000 detractors from Feb-Jun for GB, GB+, and GBX:




 

 

How to Use Pretrained Model for Inference (to Predict Classes):

To use this model for inference, a user must input the URL link to a dataset in S3

Dataset must be in csv format

Dataset must contain the following columns (syntax must be identical):

Start Date

End Date

How likely are you to recommend the Glam Bag to a friend?

What is the most important reason for your recommendation answer?

userId

NOTE: Since this is a csv, it is parsed by commas. To avoid errors, replace all commas with spaces

The user should also input the path to the saved, pretrained model that will be used for inference

Default = dbfs:/mnt/ipsy-databricks-mlp/research/ethan/monolabeled-model-business-w-flair-and-other

Click “Run All” and watch the inference occur! 

Evaluate results! Numerous bar graphs grouped by NPS, topic type, subscription, & month are displayed and help visualize trends

Some results from over 10,000 detractors from Feb-Jun for GB, GB+, and GBX:








Code:

- Notebook for training model: https://ipsy-prod.cloud.databricks.com/#notebook/4659645/command/4659655

- Notebook for inference using pretrained model: https://ipsy-prod.cloud.databricks.com/#notebook/4676157/command/4676247

- Github: https://github.com/ethanhsiao88/topic-modeling/blob/main/inference_using_model.ipynb - Connect to preview 

 


Training Pipeline:

For training the model, these are the steps for the code outlined in the notebook:

1. Read labeled data (from user-inputed S3 URL link)

2. Preprocessing (data validation, filtering only important information, adding columns)

3. Flair (filtering out only negative comments)

4. Train Model

5. Save Model

6. Evaluate Model (accuracy, f1 scores, weighted f1 score, confusion matrices)




Inference Pipeline: 

For inference using a pretrained model, these are the steps for the code outlined in the notebook:

1. Read unlabeled data (from user-inputed S3 URL link)

2. Preprocessing (data validation, filtering only important information, adding columns)

3. Flair (filtering out only negative comments)

4. Prediction using pretrained model (link to model user-inputed)

5. Evaluate Results (bar graphs grouped by NPS, topic type, subscription, & month help visualize trends)

 


Credits:

- Model built by Ethan Hsiao (ML intern) and Jyotirmoy Sundi, assisted by entire ML team

- Emails: ethanhsiao@bfaindustries.com, sundi@bfaindustries.com
