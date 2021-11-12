## Natural Language Processing on Survey Response Data
### Introduction
I recently completed a project for a global electronic retail company wanting to analyze survey data the company has conducted to 16,000 employees. As the company did not have any resources to conduct an advanced analysis on this type of data they asked for help analyzing 18 numeric responses and 2 free form responses in both a qualitative and quantiative manner. This analysis was for a presentation delivered to the C-Suite positions. 
 This article will explain the diverse capabilities of Python and its packaged libraries when it comes to doing natural language processing on free form text data as well as a diving into NLP concepts. 

### spaCy
spaCy is an open-source library using the Python programming language for advanced natural language processing. For those unfamiliar the ease of importing a complicated library like spaCy takes two lines of codes. 
![image](https://user-images.githubusercontent.com/70989415/141222950-67b1851c-55cc-4362-8330-b717a79674d8.png)
Now you can being using the features from your newly created *nlp* object. 
spaCy has become an industry standard as it differentiated itself by focusing on providing nlp software for production usage. It supports deep learning workflows through its own machine learning library, Thinc. This means it uses Thinc as its backend to support all of its NLP tasks; which will explained in this article.

### NLP Tasks
Like many other workflows within Python there is a pipeline that is followed to prepare data in order to perform a model on it. These common steps in a NLP pipeline are broken down below with supporting examples from a response taken from the Harman automotive survey. 
### Tokenization
The first step is to tokenize our text. This means we break down the paragraphs into sentences, then words and punctuations. In spaCy this is done from the below code. <br>
**Unparsed:**
![image](https://user-images.githubusercontent.com/70989415/141385843-d96a3a65-ec21-4d42-a41d-ec6491911d8d.png)
**Parsed:**
![image](https://user-images.githubusercontent.com/70989415/141385884-bb6a3e1b-f7b3-4791-b57b-bf2f2ba1786d.png)
In the examples above we are taking the the 495th survey from the Positive column in the DataFrame *example_df* and creating a new object called *sample_review*. We see in the output it shows what one of the respondents replies to "What are the strengths of Harman?". <br>
In the Parsed code we are taking this *sample_review* and attributing NLP features that were created from spaCy to create a new object *parsed_review*. The output looks the same as the Unparsed because the tokenization is taking place behind the scenes. You will see in the next examples how spaCy is breaking down this review into three sentences and then each word in order to extract the meaning from each word and how it fits into the sentences. The perfect way to visualize this is by looking at the Part-of-Speech Tagging. 
### Part-of-Speech (POS) Tagging
After tokenizing we can now tag each part of the text with its linguistic meaning as it relates to its part of speech. Below we can see each individual token in the Token column. These are all now tagged with their meaning in the Part of Sp column. By looking at the first sentence, the spaCy library knows that the word customers is a noun while the word pretty is an adjective. 
![image](https://user-images.githubusercontent.com/70989415/141386124-8cc66819-b9dd-4550-b2cb-865b8c5d5225.png)
### Lemmatization
The middle column Lemma stands for Lemmatization which is the *"use of vocabulary and morphological analysis of words, normally aiming to remove inflectional endings only and to return the base or dictionary form of a word, which is known as lemma."* - NLP Stanford Book
In the code below we see that we can now take some text and we use the nlp object to tokenize it and prepare it. Then we are going to lemmatize and also remove the standard stop words, which will be explained later. I then created an object normalize which will be used to see what this does visually. 
![image](https://user-images.githubusercontent.com/70989415/141386741-cf890564-b3d2-4477-b5e2-94ef8bace1f6.png)
We can see in the below example how the words plan / plans / planning / planned are all just different tenses of the same verb and return a base word. 
![image](https://user-images.githubusercontent.com/70989415/141386779-5e791175-b45b-4904-b9c0-46dcb7d00da6.png)
My client wanted to evaluate word usage and reduce the variability of verbs to see the most common words used in the Strength or Improvement response answers. 
### Stop Words
In the code above we saw how I used "if not token.is_stop".  What this does is remove Stop Words or words that have no meaning and don't provide meaning when doing a search query on text. Stop Words can be adjusted in spaCy settings if you would like to add or delete one of the standard Stop Words.
![image](https://user-images.githubusercontent.com/70989415/141386816-bec17261-91f1-4ba4-97d9-310ceccfbf42.png)
### Syntactic (Dependency) Parsing
It is the process of identifying sentences and assigning a syntactic structure to it. This sentence boundary detection to figure out where a sentence starts and ends is very important for NLP. spaCy provides parse trees which can be used to generate this structure below. 
![image](https://user-images.githubusercontent.com/70989415/141386868-e74aadaa-f4e2-4250-9c6a-efa76735008d.png)
### Conclusion
spaCy has become a industry standard noticed from its ease of use. The code seen above is the extent of the process needed to attribute NLP functions to your text that enable all sorts of analysis. One could now develop a multi-label convolutional neural network text classifier on their data or, in the my client's use-case, develop a topic tagging model that allows for topic usage analysis based upon a word-synonym dictionary. 
#### Works Citied
﻿https://nlp.stanford.edu/IR-book/html/htmledition/stemming-and-lemmatization-1.html
