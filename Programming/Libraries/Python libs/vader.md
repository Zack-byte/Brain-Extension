# VADER (Valence Aware Dictionary for Sentiment Reasoning)

- Sentiment Analysis
- sensitive to both polarity (positive/negative) and intensity(strength) of emotion

- sentiment score of a text can be obtained by summing up the intensity of each word in the text. 
	- "love", "enjoy", "happy", "like" all convey a positive sentiment. 
- can determine basic context
- also understands the emphasis of capitalization and punctuation such as "ENJOY"

-Main goal is to determine whether to text is positive, negative or neutral 



- also aggregate all of the sentences in a document or paragraph to arrive at an overall opinion. 

- not trying to determine the degree of positivity or negativity just whether or not it is positive or negative

- there are four scores outputted
	- negative
	- neutral 
	- positive 
	- compound (computed by normalizing the scores above) 

- it is a score assigned to the word under consideration by means of observation and experiences rather than pure logic. 

- the Valence score is measured on a scale from -4 to +4 where the lowest stands for the most Negative sentiment and the highest is the most Positive. 0 stands for neutral 

- five ways VADER classifies the input text
	- Punctuation 
		- namely the exclamation point ! increases the magnitude of the intensity without modifying the semantic orientation. 
	- Capitalization 
		- specifically using ALL-CAPS to emphasize a sentiment relevant word in the presence of other non capitalized words increases the magnitude of the sentiment intensity without affecting the semantic orientation 
	- Degree modifiers
		- impact sentiment intensity by either increasing or decreasing the intensity. e.g "The weather is extremely hot." is more intense than "The weather is hot." 
	- Polarity shift due to Conjunctions
		- the contrastive conjunction "but" signals a shift in sentiment polarity, with the sentiment of the text following the conjunction being dominant. ex "The weather is hot, but it is bearable." has a mixed sentiment, with the latter half dictating the overall rating. 
	- Catching Polarity Negation: 
		- by examining the contiguous sequence of 3 items preceding a sentiment-laden lexical feature, we catch nearly 90% of cases where negation flips the polarity of the text. for ex a negated sentence would be "The weather isn't really that hot." 

- the compound score is computed by summing the valence scores of each word in the lexicon, adjusted according to the rules, and then normalized to be between -1. this is the most useful metric if you want a single unidimensional measure of sentiment for a given sentence


- the pos, neu, neg scores are ratios for proportions of text that fall in each category 
	- these should add up to one
	- these three values are calculated by using the raw lexical scores...so if it's categorized in their dictionary as positive then it attributes to the positive percentage. 

- the compound score is a metric that calculates the sum of all the lexicon ratings which have been normalized between -1 and +1  

- this is the metric for labeling scored text
	- Positive sentiment: compound score >= 0.05
	- Neutral sentiment: 0.05 > neutral(compound score) > -0.05
	- Negative sentiment: compound score <= -0.05 