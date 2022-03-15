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

## Resultado

Visualizando a nossa matriz de confução, tivermos os seguintes resultado:

### Matriz de confusão

![regressao-logistica](https://user-images.githubusercontent.com/85235525/158451728-9d46d9bd-3ed3-4e55-a2d1-b0d798113837.jpeg)


![KNeighborsClassifier](https://user-images.githubusercontent.com/85235525/158451809-661ac581-7b39-43cb-b64a-a2fd25773417.jpeg)


![DecisionTreeClassifier](https://user-images.githubusercontent.com/85235525/158451920-af97c8b2-fb9d-4ef3-8c6f-500a11bd4641.jpeg)


![MultinomialNB](https://user-images.githubusercontent.com/85235525/158452032-a9f8bc17-9429-4ce4-bea2-7de0ab42231b.jpeg)

## Conclusão

Modelo|Seleção|Acertos(conjunto de teste)
------|-------|---------
LogisticRegression|RFE|88%
LogisticRegression|KBest|53.6%
KNeighborsClassifier|RFE|55.7%
KNeighborsClassifier|KBest|**98.5%**
DecisionTreeClassifier|RFE|*51.6%*
DecisionTreeClassifier|KBest|**100%**
MultinomialNB|RFE|*42.9%*
MultinomialNB|KBest|*54.2%*

Os melhores desempenhos ficam por conta dos modelo KNeighborsClassifier e DecisionTreeClassifier, ambos utilizando o KBest como escolha de atributos. Os piores desemprenhos foram dos modelos MultinomialNB e DecisionTreeClassifier, ambos utilizando RFE como escolha de atributos.
O objetivo principal era conseguir uma matriz de confusão o mais próximo possível de uma matriz diagonal:

![download](https://user-images.githubusercontent.com/85235525/158453594-75b17e69-7f6c-4614-b0e5-0a0114006e80.png)

# Tecnologias utilizadas

## Ferramentas

* VsCode
  * Jupyter
  * Python
      
## Bibliotecas

* Pandas
  * CSV
  * Info
  * Max
  * Corr

* Matplotlib
  * Pyplot
 
* Numpy
  * Random seed
  * Triu
  * Ones like
 
* Sklearn
  * Min Max Scaler
  * Train Test Split
  * Logistic Regression
  * *K*Neighbors Classifier
  * Decision Tree Classifier
  * Multinomial NB
  * Confusion Matrix
  * Select *K*Best
  * Chi2
  * RFE

* Seaborn
  * Heatmap


# Autor

<a href="https://www.linkedin.com/in/mikeias-o-5a4b2a184/"><img src="https://camo.githubusercontent.com/4754d9b981ccaa192658e293fa6ab42b543520e7ad39756929edc7e95fca43aa/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f2d4c696e6b6564696e2d3065373661383f7374796c653d666c61742d737175617265266c6f676f3d4c696e6b6564696e266c6f676f436f6c6f723d7768697465266c696e6b3d4c494e4b2d444f2d5345552d4c494e4b4544494e" alt="linkedin" width="100"></a> <a href="mailto:mikeias.d.s.o@gmail.com"><img src="https://camo.githubusercontent.com/0137b0e6dbd05bb3986fa835806ca7b044f5cdaab7e4c8af8829ceec61195346/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f2d476d61696c2d4646303030303f7374796c653d666c61742d737175617265266c6162656c436f6c6f723d464630303030266c6f676f3d676d61696c266c6f676f436f6c6f723d7768697465266c696e6b3d4c494e4b2d444f2d5345552d454d41494c" alt="gmail" width="85">

# Licença

MIT License

Copyright (c) 2022 xpcosmos

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.






