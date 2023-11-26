# train-ner-model-with-spacy
Custom training NER model with spacy library and annotaded dataset in JSON 

To train and use model prepare dataset like one attached in data.json file. 
You can use https://github.com/doccano/doccano browser tool for this purpose. 

### Part I: Label data
Dataset was prepared based on https://www.kaggle.com/datasets/kaushiksuresh147/bitcoin-tweets
To prepare tagged dataset run steps below:

#### 1. Download and install browser program for labeling data "doccano":
go to link below and run described steps:
https://github.com/doccano/doccano
```
# install doccano
pip install doccano
# Initialize database.
doccano init
# Create a super user.
doccano createuser --username admin --password pass
# Start a web server.
doccano webserver --port 8000
# Start the task queue to handle file upload/download (separate console session).
doccano task
```

Open doccano in browser using  http://127.0.0.1:8000/.
#### 2. Create new project:
Mark "Sequence Labeling"
Add some project name and description
Check options: "Allow single label" and "Randomize document order"

#### 3. Import dataset:
From left menu choose option "Dataset" and Actions/Import Dataset.
In "File format" select "TextLine"
Upload file bitcoin_tweets_text_lines.txt
Click "Import" and wait until file is imported

#### 4. Add labels:
From left menu choose option "Label".
Add labels as below, by clicking Actions/Create Label:
- Cryptocurrency name
- Cryptocurrency rate
- Organisation
- URL
- Emoticon
- Date

#### 5. Annotate data:
On left sidebar click "Start Annotation" and tag all texts by marking each meaningfull phrase that belongs to one of created categories.

#### 6. Export training set:
From left menu choose option "Dataset" Actions/Export Dataset.
In "File format" select "JSONL"
Unzip created file and copy .jsonl file into project dir.


### Part II: Train model
To use training set from previous part (Label data) you need to change jsonl file into json.
You can achive it by adding comma in all lines except last one and wrap everything in square braces, see samples.json as example.

To train model open doccano-spacy.ipynb in jupyter lab  and run all cells.
Replace samples.json with bitcoin_tweets_text_lines.json to train model on prepared dataset.
Replace also labels with ones used for annotation.