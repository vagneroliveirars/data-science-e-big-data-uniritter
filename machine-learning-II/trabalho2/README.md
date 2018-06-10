# Classificação de imagens

Classifica uma imagem contendo um cachorro ou um gato usando o dataset do Kaggle <a href="https://www.kaggle.com/c/dogs-vs-cats-redux-kernels-edition/data">Dogs vs. Cats Redux: Kernels Edition</a>.

## Classificação de imagens.ipynb:
Utilizando uma rede neural convolutiva (CNN), o modelo atingiu uma acurácia de 62%.

Utilizando uma rede MobileNet v2, o modelo atingiu uma acurácia de 60%.

Foram utilizadas 6000 amostras para treino, 1000 amostras para validação e 1000 amostras para teste.

Estrutura de diretórios do projeto:

* project
  * data
    * train
      * dogs
      * cats
    * validation
      * dogs
      * cats
    * test

Separação das imagens para treino:

```sh
$ find train/cat.* -maxdepth 1 -type f |head -3000|xargs mv -t data/train/cats/
```

```sh
$ find train/dog.* -maxdepth 1 -type f |head -3000|xargs mv -t data/train/dogs/
```

Separação das imagens para validação:

```sh
$ find train/cat.* -maxdepth 1 -type f |head -500|xargs mv -t data/validation/cats/
```

```sh
$ find train/dog.* -maxdepth 1 -type f |head -500|xargs mv -t data/validation/dogs/
```

Separação das imagens para teste:

```sh
$ find test/* -maxdepth 1 -type f |head -1000|xargs mv -t data/test/
```

