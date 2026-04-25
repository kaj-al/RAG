# RAG Documentation
This repository consists basics of RAG concept including Data Loading, 

## Data Loading

1. Text Loader
```python
from langchain_community.document_loaders import TextLoader

loader = TextLoader("file.txt")
text = loader.load()  #Load data
```
2. PDF Loader
```python
from langchain_community.document_loaders import PyPDFLoader

loader = PyPDFLoader("file.pdf")
pdf = loader.load()
pdf[0].page_content  # Content of first page
len(pdf)   # total pages
```
3. CSV Loader
```python
from langchain_community.document_loaders import CSVLoader

loader = CSVLoader("file.csv")
csv = loader.load()
```
4. WebPage Loader
```python
from langchain_community.document_loaders import WebBaseLoader

loader = WebBaseLoader("/")
web = loader.load()
```
5. WikiPedia Loader
```python
from langchain_community.document_loaders import WikipediaLoader

loader = WikipediaLoader("",load_max_docs=2)
wiki = loader.load()
```

## Text Splitting
chunk size = how many characters are in one chunk .

chunk overlap = how many characters of previous chunk are overlap in next chunk
1. Text splitter
```python
from langchain_text_splitters import RecursiveCharacterTextSplitter

texts = ""
splitter = RecursiveCharacterTextSplitter(chunk_size=,chunk_overlap=)  
chunks = splitter.split_text(texts)
```

2. Documents splitter
```python
from langchain_community.document_loaders import PyPDFLoader
from langchain_text_splitters import RecursiveCharacterTextSplitter

loader = PyPDFLoader("file.pdf")
docs = loader.load()
splitter = RecursiveCharacterTextSplitter(chunk_size=,chunk_overlap=)
chunks = splitter.split_documents(docs)
``` 

### Vector Embeddings

We can use any embedding model here i choose OpenAI models 
```
text-embedding-3-small = 1536 length
text-embedding-3-large = 3072 length
```
```python
# API key load
from dotenv import load_dotenv
load_dotenv()

from langchain_community.document_loaders import PyPDFLoader
from langchain_text_splitters import RecursiveCharacterTextSplitter
from langchain_openai import OpenAIEmbeddings

docs = [] 
embeddings = OpenAIEmbeddings(model="")
vector = embeddings.embed_documents(docs)
len(vector)     # length of whole vector
len(vector[0])   #if you want to print first index length 
```
### Vector Store
```python
from langchain_chroma import Chroma

store = Chroma.from_texts(
    texts = ,
    embedding = ,
    persist_directory = "./vector_db" #to store it locally
)
```

## Documentations
- [Document Loader Integrarions](https://docs.langchain.com/oss/python/integrations/document_loaders)
- [Text Spliiter Integrations](https://docs.langchain.com/oss/python/integrations/splitters)
- [Embedding Models](https://docs.langchain.com/oss/python/integrations/embeddings)
- [OpenAI Embeddings](https://docs.langchain.com/oss/python/integrations/embeddings/openai)
- [Vector Store](https://docs.langchain.com/oss/python/integrations/vectorstores)

## Contents
- `data_load.ipynb` - How to Load Data
- `split.ipynb` - Split Loaded Data
- `embedding.ipynb` - Embeddings of Loaded Data and how to store Data in Vector Db 
