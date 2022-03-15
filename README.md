# Modelo de classificação: Aprendizado supervisionado para predição da qualidade de vinhos

## Introdução

O mercado de vinhos tem crescido no Brazil apesar da crise econômica que está ocorrendo. Segundo uma matéria realizada pelo portal G1 de notícias, houve um crescimento de 26% no setor e mais que nunca os consumidores procuram não somente o consumo casual da bebida, mas a apreciação do produtos como um hobbie (MARTINS, 2022).
Visando o supracitado, esse projeto busca classificar a qualidade dos vinhos através de dados referentes a testes físico-químicos fornecidos pelo portal Kaggle.

## Análise inicial dos dados

Para o início da construção do projeto, vamos realizar a importação da base de dados e traduzir todos os atributos - colunas - dessa base. 

Atributos|
---------|
Acidez fixa|
Acidez volátil|
Ácido Cítrico|
Açucar residual|
Cloretos|
Dióxido de enxofre livre|
Total dióxido de enxofre|
Densidade|
pH|
Sulfatos|
Álcool|
Qualidade|
ID|

Através do método de informações da biblioteca Pandas, foi possível constar que não existem dados nulos, portanto, podemos prosseguir com os processos.

# Pré processamento

## Redução de dimensionalidade

Para uma maior taxa de sucesso de baixa generalização do modelo de aprendizado, vamos realizar uma redução da dimensionalidade. Primeiro iremos gerar matrizes de correlação para a remoção de dados altamente correlacionados.

### Matrizes de correlação

![1f04af4e-d736-4f89-95c6-6f372c169f1f](https://user-images.githubusercontent.com/85235525/158412204-c71f1541-0773-466e-926d-50ebc30e4e49.png)

Encontramos alguns dados altamente correlacionado. Vamos remover alguns deles. Os escolhidos para a remoção foram:

Removidos|
---------|
Acidez fixa|
Total dióxido de enxofre|
Ácido cítrico|
ID|
Álcool|

Após a remoção desse atributos tivemos a seguinte matriz de correlação 

![141a3576-b970-4ab8-a1ae-d3a51fc4bd4b](https://user-images.githubusercontent.com/85235525/158412724-18ea21d9-789a-48de-a137-32b8d1abd7ad.png)

### Normalização dos dados

Para a garantia de que o modelo irá de comportar de uma forma satisfatória, vamos realizar uma normalização através do método do Sklearn [MinMaxScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.MinMaxScaler.html).

### Criação do modelo

Para a criação do modelo, vamos testar diferentes algorítimos. Vamos definir uma SEED, ou semente de aleatóriedade para que seja possível a reprodução dos testes. Para esse modelo foi definida a semente **585**.

Algorítimos|Função|
-----------|------|  
Regressão logística|Classificador|           
Classificador de K vizinhos|Classificador|
Árvore de decisão|Classificador|
Nayve Bayers Multinomial|Classificador|
RFE|Seleção de atributos|
Select KBest|Seleção de atributos|

Vamos separar 30% dos dados para teste e 80% dos dados para treino.
Antes de treinarmos o modelo, vamos utilizar diferentes algorítimos para a relação dos atributos e testar eles.


