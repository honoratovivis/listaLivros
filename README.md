# Olha eu aqui aprendendo a tratar dados 

## Treino de hoje requer o básico para o MongoDB então eu vou :
- Inserção de documentos
- Atualização de documentos
- Exclusão de documentos
- Consulta com projeção
- Consulta utilizando combinação entre os seletores
- Consulta paginada e ordenada (utilizar skip, limit e sort)
 
## para isso criei um `JSON` com alguns livros  para um diário de leitura pessoal 
### Ele contém :
```javascript
{
   "nome": string,
   "Autor": string,
   "Categoria":string,
   "Número de páginas": number,
   "Gostou": boolean,
   "Lido": boolean
}
```
---
## Criado o `JSON` eu segui o passo a passo :
### 1- Inicializei o mongoDB no `Pronpt de Comando`
### 2- em um novo `Pronpt de Comando` usei o comando ```use diarioDeLivros ``` para criar o novo banco de dados  e o  ```db.createCollection``` para criar a coleção `lista`.
### 3-  agora já no Robo3T eu criei  uma `collection` dentro de `lista` chamada `livros` para armazenar os livros que estão listados no arquivo ```livros.json```.
### 4- inseri todos os livros listados no ```livos.json```
### 5- Atualizei o número de páginas dos livros com as instruções 
``` javascript
db.getCollection('livros').update(
    {
    "Nome": "1984"
    },
    {$set: 
        {
            "Número de paginas": '308'
            }
    }
)
```
``` javascript
db.getCollection('livros').update(
    {
    "Nome": "Admirável Mundo Novo "
    },
    {$set: 
        {
            "Número de paginas": '312'
            }
    }
)
 ```
``` javascript
db.getCollection('livros').update(
    {
    "Nome": "Frankenstein"
    },
    {$set: 
        {
            "Número de paginas": '136'
            }
    }
)
 ```
``` javascript
db.getCollection('livros').update(
    {
    "Nome": "Jogador Número 1"
    },
    {$set: 
        {
            "Número de paginas": '462'
            }
    }
)
 ```
``` javascript
db.getCollection('livros').update(
    {
    "Nome": "Assim Falou Zaratustra"
    },
    {$set: 
        {
            "Número de paginas": '532'
            }
    }
)
 ```
``` javascript
db.getCollection('livros').update(
    {
    "Nome": "Uma história feita por mãos negras"
    },
    {$set: 
        {
            "Número de paginas": '272'
            }
    }
)
 ```
### 6- A exclusão de documentos eu fiz com duas variantes
*  `Autor` 
``` javascript
db.getCollection('livros').remove(
    {
        "Autor": "Niccolò Machiavelli"
    }
);
```
 * `Categoria`
``` javascript
db.getCollection('livros').remove(
    {
        "Categoria":"Ficção Politica"
    }
);
```
### 7- Para Consulta com projeção usei 
``` javascript
db.getCollection('livros').find(
    {},
    {
        "Categoria" : 1, "_id" : 0
    }
)
```
### 8- Para consulta utilizando combinação entre os seletores usei 
``` javascript
db.getCollection('livros').find(
    { 
        "Categoria":"Ficção Filosófica",
        "Autor": "Friedrich Nietzsche"
     }
).pretty()
```
 
``` javascript
db.getCollection('livros').find(
    { 
        "Categoria": "Ficção Científica",
        "Autor": "Douglas Adams",
        "Número de paginas": 208
     }
).pretty()
```
``` javascript
db.getCollection('livros').find(
    { 
        "Nome": /.*mochileiro.*/,
        "Autor": "Douglas Adams",
        //"Número de paginas": 208
     }
).pretty()
 
```
Você pode tirar o comentário para observar um filtro melhor 
### 9- Para Consulta paginada e ordenada usei 
* skip
```javascript
db.getCollection('livros').find(
    {
        "Número de paginas": 208
    }
).skip(2)
```
* limit
```javascript
db.getCollection('livros').find(
    {
        "Número de paginas": 208
    }
).limit(1)
 ```
* sort
    - *decrescente*
```javascript
db.getCollection('livros').find(
    {
        "Autor": "Douglas Adams"
    }
).sort(
    {
        "Número de paginas": -1
        }
)
```
* sort
    - *crescente*
    
```javascript
db.getCollection('livros').find(
    {
        "Autor": "Douglas Adams"
    }
).sort(
    {
        "Número de paginas": 1
        }
)
```

* Também combinei os argumentos 

```javascript
db.getCollection('livros').find(
    {
        "Número de paginas": 208
    },
    {
        skip: 3, 
        limit: 5
    }
)
``` 
### 10- E só pra testar eu filtrei por uma quantidade específica de páginas 
``` javascript
db.getCollection('livros').find( 
    { 
        "Número de paginas" : {
            "$gte" : 112 , 
            "$lte" : 224
        } 
    } 
)
 ```
 # *ESTÁ FEITO*
 
 ## ATÉ A PRÓXIMA 
![Alt Text](https://media.giphy.com/media/IL4iTvQH0MjS/giphy.gif)
