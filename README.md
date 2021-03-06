# Vetor de Palavras
Projeto para gerar vetor de palavras em Django + Django Rest Framework para processamento de linguagem natural.  A maior parte do NLP([Natural Language Processing) foi feita utilizando a biblioteca **nltk** do python.

# Porque utilizar a biblioteca **nltk**?
**nltk** é um conjunto de bibliotecas e programas para processamento simbólico e estatístico da linguagem natural, algumas suas bibliotecas atendem perfeitamente as necessidades do projeto como **stopwords** , **punkt**.
Para instalar as dependências basta executar no python:
> import nltk
> nltk.download(stopwords)
> nltk.download(punkt)

## Rodando o projeto
Após instalar as dependência para rodar o projeto execute os comandos dentro da pasta API
*Instalar todas as dependências nessesárias do python*
> pip install -r requirements.txt

Gerar o banco de dados
> python manage.py migrate

Rodar o servidor
> python manage.py runserver

Rodar testes
> python manage.py test

## Natural language processing

### Endpoints
***{host}/words_vector/***
| URL |METHOD|PARAMS|
|--|--|--|
| /file-vocabulary|POST|Multipart Form(files)|
| /file-two-grams-vocabulary|POST|Multipart Form(files)|
| /file-two-grams-vector|POST|Multipart Form(files)|
| /file-vectors|POST|Multipart Form(files)|
| /file-vocabulary-nostop|POST|Multipart Form(files)|
| /file-vector-nostop|POST|Multipart Form(files)|


### Exemplos de chamadas
#### {host}/words_vector/file-vocabulary
Retorna o vocabulário gerado com as palavras únicas de todos os arquivos
Data:
Method: POST
Type: Multipart Form

    file1     file1.txt
    file2     file2.txt

Response:

    {
	  "vocabulary": [
	    "falar",
	    "é",
	    "fácil",
	    "mostre",
	    "me",
	    "o",
	    "código",
	    "escrever",
	    "difícil",
	    "que",
	    "funcione"
	  ],
		  "words": 11
	  }




#### {host}/words_vector/file-two-grams-vocabulary
Retorna o vocabulário gerado com as palavras únicas de todos os arquivos
Data:
Method: POST
Type: Multipart Form

    file1     file1.txt
    file2     file2.txt

Response:

    {
        "falar é",
        "é fácil",
        "fácil mostreme",
        "mostreme o",
        "o código",
        "código é",
        "fácil escrever",
        "escrever código",
        "código difícil",
        "difícil é",
        "é escrever",
        "código que",
        "que funcione"
    ],
	    "words": 13
    }


#### {host}/words_vector/file-two-grams-vector
Retorna o vetor das palavras do vocabulario 2grams
Data:
Method: POST
Type: Multipart Form

    file1     file1.txt
    file2     file2.txt

Response:

    [
	    {
	    "name": "teste.txt",
	    "vector": [1,1,1,1,1,1,0,0,0,0,0,0,0,0]
	  },
	  {
	    "name": "teste2.txt",
	    "vector": [0,1,0,0,0,0,0,1,2,1,1,1,1,1]
	  }
	]

#### {host/words_vector/file-vectors
Retorna o vetor das palavras do vocabulario
Data:
Method: POST
Type: Multipart Form

    file1     file1.txt
    file2     file2.txt

Response:

    [
	  {
	    "name": "teste.txt",
	    "vector":  [1, 1, 1, 0, 0, 1, 1, 0, 0, 0, 0]
	  },
	  {
	    "name": "teste2.txt",
	    "vector":  [0, 2, 1, 0, 0, 0, 2, 2, 1, 1, 1]
	  }
	]


#### {host}/file-vocabulary-nostop

Retorna o vocabulário gerado com as palavras únicas de todos os arquivos removendo stopwords
Data:
Method: POST
Type: Multipart Form

    file1 file1.txt
    file2 file2.txt


Response:
    {

    "vocabulary": [
	    "falar",
	    "fácil",
	    "mostre",
	    "código",
	    "escrever",
	    "difícil",
	    "funcione"
    ],
    "words": 7

    }

#### {host}/file-vector-nostop

Retorna o vetor das palavras do vocabulario removendo stopwords

Data:
Method: POST
Type: Multipart Form

    file1 file1.txt
    file2 file2.txt

Response:

        [
    	  {
    	    "name": "teste.txt",
    	    "vector": [1,1,0,1,0,0,0]
    	  },
    	  {
    	    "name": "teste2.txt",
    	    "vector": [0,1,0,2,2,1,1]
    	  }
    ]


# Django Admin Painel
### Logs dos dados processados
#### {host}/admin/words_vector/logs/
![enter image description here](https://i.ibb.co/8gHmf0x/image.png)
