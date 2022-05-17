# LDA (Latent Direchlet Allocation)

Topic modeling is an unsupervised machine learning technique that's capable of scanning a set of documents, detecting word and phrase patterns withing them and automatically clustering word groups and similar expressions that best characterize a set of documents 

Topic classification is a supervised machine learning technique one that needs training before being able to automatically analyze texts. whereas...
Topic modeling is an unsupervised machine learning technique 
TM: is a machine learning technique that automatically analyzes text data to determine cluster words for a set of documents Since topic modeling doesn't require training it's a quick and easy way to start analyzing your data however you can't guarantee you'll receive accurate results, which is why many busnesses opt to invest time training a topci classification model . 

TC: are known as supervised machine learning techniques needs to know the topics of a set of texts before analyzing them using these topics data is tagged manually so that a topic classifier can learn and later make predictions by itself. 

Topic modeling involves counting words and grouping similar word patterns to infer topics within unstructured data. detects patterns such as word frequency and distance between words a topic model clusters feedback that is similar nd words and expressions that appear most often with this information you can quickly deduce what each set of texts are talking about 

topic modeling refers to the process of dividing a corpus of documents in two: 
1. a list of the topics covered by the documents in the corpus
2. several sets of documents from teh corpus grouped by the topics they cover. 

the underlying assumption is that every document comprises a statistical mixture of topics i.e. a statistical distribution of topics that can be obtained by ading up all of the distributions for all the topics covered what topic modeling methods do is try to figure out which topics are present in the documents of the corpus and how strong that presence is . 


LSA: Latent Semantic Analysis is one of the most frequent topic modeling methods analysts make use of it is based on what is known as the distributional hypothesis which states that the semantics of words can be grasped by looking at the contexts the words appear in in other words, under this hypothesis the semantics of two words will be similar if they tend to occur in similar contexts. that said LSA computes how frequently words occur in the documents and the whole corpus and assumes that similar documents will contain approximately the same distribution of word requencies for certain words in this case syntactic information and semantic information the multiplicity of meanings of a given word are ignored and each document is treated as a bag of words. 

LDA: Latent Direchlet Allocation is based on the same underlying assumptionos as LSA: the distributional hypothesis i.e similar topics make use of similar words and the statistical mixture hypothesis i.e documents talk about several topics for which a statistical distribution can be determined the purpose of LDA is mapping each document in our corpus to a set of topics which covers a good deal of the words in teh document. 

what Lda does in order to map the documetns to a list of topics is assign topics to arrangements of words e.g n-grams such as best player for a topics related to sports 

you can think of topic modeling as : 
Dimensionality reduction where rather tahn representing a text Tin its feature spcae as 

Unsupervised Learning where it can be compared to clustering as in teh case of clustering the number of topics like the jmber of clusters is an output parameter by doing topic modeling we build clusters of words rather than clusters of texts 

Tagging abstract topics that occur in a clooetion of documents that best represents the information in them .