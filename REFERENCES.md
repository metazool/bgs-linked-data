# References for GBDB talk on Text Mining and Linked Data at BGS


## Stanford NER

https://nlp.stanford.edu/software/crf-faq.shtml - gives a good outline of training a custom NER model on sentences annotated with extra properties (e.g. taxonomic names).


"The training data should be in tab-separated columns, with minimally the word tokens in one column and the class labels in another column." You could do the tokenisation with CoreNLP or equally with spacy.io. Include punctuation tokens on separate lines, and label everything that you *dont* want to include in your custom model with 'O' (for other)


https://stanfordnlp.github.io/CoreNLP/corenlp-server.html - our first prototypes were done with the Java API but later version done with the CoreNLP server web-based API, which we were recommended as being a lot faster. There is material at BGS both for simplifying the raw output from the server, and configuring it to add a custom model as well as the standard english NER model.

## Spacy.io

https://spacy.io/usage/training#section-ner - same sort of data structure but with a different layout, as a JSON file with a set of strings and the entity tags assigned to character offsets within each string. I didnt do much more than re-run the examples on this page over our data, trying with a blank model (which didnt have enough knowledge of general NER to find specific entities) and with a pre-trained English one (a balance of about 1/4 regular rather than custom sentences seemed to be needed to avoid the 'catastrophic forgetting' as outlined here. I would love to revisit the approach.


## Linked Data

When named entities are extracted and then linked to our Linked Data, it's done by string comparison using Levenshtein distance, e.g. https://pypi.org/project/python-Levenshtein/
We have a simple web service which looks up similar entities and optionally tries to georesolve locations which can be handed the NER output. This didn't require a triplestore, bt a simple CSV cross-referencing URIs with taxonomic names.

For links to taxonomic terms in palaeobiology we'd like if possible to use a URI scheme based on mikrotax.org and get an export of RDF data directly from mikrotax





