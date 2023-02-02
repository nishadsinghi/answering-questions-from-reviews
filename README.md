The aim of this project is to create a pipeline to automatically answer user questions about products using review from other users. This happens in two stages:
* ```Retriever:``` The retriever selects the most relevant reviews given the question. First, it uses a bi-encoder to compute the embeddings of all reviews and the question. \
Then, the question is compared to all reviews using cosine similarity. It selects the top-k (say, top 100) reviews for the given question with the highest cosine similarity. \
However, the bi-encoder sometimes returns reviews that are not relevant to the question. Due to this reason, the selected reviews are re-ranked to sort them based on how relevant they are. \
This is done using a cross-encoder. 
* ```Reader:``` The reader is used to extract the answer to a given question from a given review. 

This project is built for the ```subjQA``` dataset, which consists of user reviews in English for products and services in various categories.

## The retriever
The retriever is based on the ```multi-qa-MiniLM-L6-cos- v1``` bi-encoder + ```cross-encoder/ms-marco-MiniLM-L-6-v2``` cross-encoder, both fine-tuned on ```subjQA``` dataset. \
I also compare performance with pre-trained models as a baseline. \
The metric used to evaluate the performance of the retriever is ```recall```, which is the fraction of the reviews returned by the retriever that were relevant to the question.

## The reader
The reader is based on the ```deepset/minilm-uncased-squad2``` model, fine-tuned on ```subjQA```. I compare the performance of the fine-tuned model with the pre-trained model in terms of the F-1 Score.

