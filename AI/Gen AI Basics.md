### GenAI Evolution

**Statistical ML** - predicting outcomes based on parameters(Features)  - Structured data

Problem

Image Reconginition - Identifying if the image is cat and dog - Complex Features, bunch of Pixel (Unstructured data)

Came **Deep learning** for that consists of Neural Networks
Recurrent Neural Networks (RNN)

Want to translate sentence from language to other - rnn 
generative in nature - autocomplete based on the content - Email autocomplete 

Do by predicting probability for next word or sentence.

**Language Model** - Is an AI model that can predict the next word(or set of words) for a given sequence of words.

Train neural network 
Self-Supervised Learning 


When you have so many layers into the neural networks we get LLM(Large Language Model).

GPT-4 175 Billion Parameters

Transformer - Special neural network architecutre

Statistical ML -> Neural Networks -> RNN -> Transformers

Transformers 
e.g. Text Models - BERN, GPT
Image Models - DALL-E, Stable Diffusion

GPT - Generative Pre-trained Transformer

On top Statistical Predictions  LLM uses another Approach called Reinforcement Learning with Human Feedback (RLHF).

To make models less toxic as they don't have emotions, subjective experience.


## Embeddings and Vector database

Embeddings - numeric representation of text in form of a vector such that you can capture the meaning of that text. 
Once you create embedding for that text you can do math with the words and sentences.

Vector database allows to store these embeddings and perform efficient search on these embeddings 

Calories in apple and Employees in Apple - Google search 

How google figures out between fruit and company ? 
**Semantic Search** - Not searching by keyword but understanding the intent of user query.

For performing semantic search embedding is used

e.g - King - woman + woman = Queen

### Word Embedding techniques

CBOW, Skip gram - Word2vec, GloVe, fastText
Based on transformer architecture - BERT, GPT
Based of LSTM - ELMo

## Retrieval Augmented Generation (RAG)

Used to train LLM for our organisational or private data.

Open source - LLama2

### Langchain

Popular python library that makes building LLM (GenAI) apps easier

Tools required- 
GPT Model
Cloud service 
LangChain, Pytorch, TensorFlow

Workflow: 

Documents --> Chunk Splits --> VectorDB --> Retrieval --> Prompt (passing chunks to openAI call)







