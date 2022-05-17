# Prodigy ML Tool
Prodigy: 

-Notes: 
	- Annotation tool used to help with data tagging
	- assists with the preparation of data used for ML Model training
	- Allows for fine tuning in areas such as NER where custom tags are often needed in certain implication areas


Commands: 
	- to make corrections on an existing models predictions 
		- python -m prodigy ner.correct ner_smart_messages en_core_web_sm ./MessageData.Json --labels PERSON,ORG,LOC --unsegmented

	- to train model: 
		- python -m prodigy train ner ner_smart_messages en_core_web_sm 


Manual annotation with patterns: 
	- to annotate with patterns you'll need a patterns file a spacy model for tokenization or your own custom tokenizer and a source of input text 

using the ner.manual we can now stream in and annotate the data all pattern matches will be pre-=highlighted in the UI so we only need to make corrections unselect wrong or incomplete matches and add the entities that the patterns missed 

Match patterns are typically provided as a JSONL file and can be used to prehighlight spans for faster and more efficient annotation. If you have words and phrases that you know are pretty much always an entity you can use patterns so you only have to annotate the exceptions 

for using patterns use this command in the cmd line: 

python -m prodigy ner.manual ner_smart_test en_core_web_sm
 


Token patters: These patterns are lists of dictionaries with one dictionary describing one token to match. The token attributes to match on can be the token's text or lowercase form lower but also lexical attributes like is_punct or linguistic features like lemma or pso 


prodigy bert.ner.manual ner_reddit ./reddit_comments.jsonl --label PERSON,ORG --tokenizer-vocab ./bert-base-uncased-vocab.txt --lowercase --hide-wp-prefix -F transformers_tokenizers.py




the great thing about using prodigy is that all we have to do when we train the model is just plug it in to predict. and not much extra work on that side of the token 

Topic Modeling is a type of statistical modeling for discovering the abstract topics that occur in a collection of documents

First in first out: is an asset-management and valuation method in which assets produced or acuired first are sold used or dispose of first. 

Azure Service Bus: 
	- Messaging: Transfer business data, such as sales or purchase orders journals, or inventory movements. 
	- Decouple applications
	- load balancing
	- topics and subscriptions
	- transactions
	- message sessions

Logstash is a light-weight open source server side data processing pipeline that allows you to collect data from a variety of sources, 

- Kibana is a data visualization dash board software for elastic search it provides visualization capabilities on top of te content indexed on a elastic search cluster 

Transport Layer Security 

Site to Site is a connection between two networks


Data at rest in information technology means data that is housed physically on computer data storage in any digital form. Data at rest includes both structured and unstructured data. 


FIPS Compliant = Federal Information Processing Standards in order to act in accordance with the Federal Information Security Management Act of 2002 and the Federal Information Security Modernization Act 

1. create a phrase list or match patterns 
2. label data with help of patterns
3. train temporary model 
4. label more by correcting model 

Spacy sense2vec,: is a new twist on word2vec that lets you learn more interesting detailed and context sensitive word vectors. 

the problem with word2vec: when humans write dictionaries and thesauruses we define concepts in relation to there concepts 
in nlp it's often more effective to use dictionaries that define concepts in terms of their usage statistics. word2vec family of models are the most popular way of creating these dictionaries. 

Word2vec gives you a dictionary where each definition is just a row of say 300 floating point numbers to find out whether two entries in the dictionary are similar you ask how similar their definitions are 

the problem with word2vec is the word part. consider a word like duck no individual usage of the word duck refers to the concept
we should allow word vectors to grow arbitrarily so that we can do a better job of modelling complicated concepts what we want to do is have different vectors for the different senses we also want a simple way of knowing which meaning a given usage refers to    for this we need to analyse token in context.


Sense2vec: follows Transaction in adding part of speech tags and named entity labels to the tokens. additionally merge named entities and base noun phrases into single tokens so that they receive a single vector 

the vector space seems like it'll give a good way to show compositionality: 
A phrase is compositional to the extent that its meaning is the sum of its parts. The word vectors give us good insight into this. the model knows that fair game is not a type of game

so the vectors approach should provide better predictions then the standard ml models because they take into account context of the word and the entire sentence as a whole 


- sense2vec word vector package. is a twist on teh word2vec models that are used to create word vector spaces that include semantic context. incorporates neural word representations to gather even more context.


The modeling process is as follows: 
- create seed terms. we use these as a starter for creating our entity annotations
- gather our entity annotations using prodigy and save them to a .jsonl file. 
- use our entity annotations to train the ner portion of the spacy pipeline we train the model using the actual text we are analyzing, in this case the 3000 reddit submission titles. 
- pickle our model and run a train test split
- run a train curve test to see if the model will benefit from further training
- decide whether we are satisfied with the model metrics and if continuing on teh current path is justified., 


Prodigy terms.teach the vectors variable specifies which word list you want to use.  
the seeds variable gives prodigy a place to start it's like saying to prodigy i'm looking for something kinda like this and then prodigy focuses in on those words to search for entity examples we want to capture. After executing the above command you can then use your web 


python -m prodigy train component datasets spacy_model --init-token2vec --output --eval-id --eval-split --n-iter --batch-size --dropout --factor --textcat-exclusive --ner-missing --binary --silent 

the train method takes all the information we've collected and uses it to train the spacy pipeline. this method takes our previously create database language model pretaining file and output file path and a test train split ration 

prodigy provides a great method called train-curve specifically designed to help answer the question regarding whether to continue to train our model or try another approach. this method creates four models with 25 percent 50 percent 75 percent and then 100 percent of our data. the goal is to see how well the model improves as we give it more data we can see form the above metrics that in the last step our accuracy increases. this typically meas that training the model further with more examples will increase the models accuracy. remember that we are looking for entities that are text examples of misinformation even when pulling data from conspiracy on reddit a place rife with misinformation picking up the signal of misinformation is ver difficult.