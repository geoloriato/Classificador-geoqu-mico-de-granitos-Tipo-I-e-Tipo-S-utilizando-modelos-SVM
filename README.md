# Classificador geoquímico de granitos "Tipo I" e "Tipo S" utilizando modelos SVM

**Aluno:** Guilherme Loriato Potratz

**Orientadora:** Manoela Kohler


# 1. Introdução

Os granitoides exibem aspectos estruturais, texturais, mineralógicos e geoquímicos altamente variáveis, o que demonstra que estas rochas podem ter sua origem associada à diversos processos petrogenéticos e ocorrem nos mais distintos ambientes geotectônicos. Essa diversidade proporcionou o surgimento de uma série de classificações para os granitoides. Sendo uma das mais importantes a classificação em granitos “Tipo I” e “Tipo S”, uma classificação clássica que introduz o conceito da dualidade dos granitos e leva em consideração sua gênese.

A classificação dos granitos em “Tipo I” e “Tipo S” foi proposta por Chappel & White (1974), baseado em estudos de granitos da Zona Orogênica de Tasman (sudeste da Austrália). Os granitos “Tipo S” resultam da fusão parcial de rochas de origem sedimentar e os granitos “Tipo I” da fusão parcial de rochas metaígneas.
Dentre as características dos elementos maiores, destacam-se:

 - Granitos tipo I tem um amplo intervalo de sílica (55% - 76%), já em granitos tipo S a sílica é superior a 65%;
 - O índice A/CNK dos granitos tipo I é, geralmente, inferior a 1,05, já em granitos tipo S o índice A/CNK é superior a 1,05;
 - Granitos tipo I apresentam valores maiores de Ca, Na e K;
 - Granitos tipo S são mais ricos em Al
 - 
Da mesma maneira, os elementos traços e terras raras também apresentam comportamento distinto nos dois tipos de granitos. Granitos tipo S são ricos em Rb e metais de transição (Pb, Cr e Ni) e pobres em Sr, Cu, e Mo.

Em relação à essa classificação, é importante enfatizar que a distinção entre os tipos I e S, ainda que fundamentada em critérios observacionais, é essencialmente genética e conceitual. Diante do avanço de estudos em granitoides, a classificação destas rochas nos tipos I e S tem sido reavaliada, não podendo ser feita apenas pela mineralogia primária e o índice de saturação de alumina conforme proposto por Chappell & White (1974). Gao et al. (2016) e Gao et al. (2017) destacam que essa dificuldade em aplicar a classificação em tipos I e S se deve ao fato de que as características de granitos altamente diferenciados se sobrepõem, havendo então a necessidade de avaliar características que vão além da composição mineralógica e do índice de saturação em alumina.

Considerando que as principais metodologias que adotam análises litogeoquímicas são anteriores à década de 1990 e consideram apenas 2 ou 3 elementos para a classificação, este trabalho se propõe a treinar um modelo de classificação para granitos tipo I e S com base em todos os óxidos e em alguns elementos traços e terras raras. Para isso, foram compiladas análises litogeoquímicas de trabalhos consagrados nos dois tipos de granitos.


# 2. Modelos

Foram testados 3 modelos de Machine Learning para classificação supervisionada (Decision Tree, Random Forest e SVM), sendo adotado o modelo SVM por apresentar as melhores métricas de avaliação.

## 2.1. Parâmetros do modelo

A seleção dos melhores parâmetros para o modelo foi feita com o GridSearchCV, da biblioteca sklearn. Os melhores parâmetros encontrados para o modelo são:

 - Kernel polinomial;
 - C=10, dregree = 4;
 - Gamma=0,01.

## 2.2. Modelos treinados

Foram treinados três modelos distintos, sendo eles:

 - Modelo A - Apenas com os óxidos: SiO2, Al2O3, Fe2O3, MgO, CaO, Na2O, K2O, TiO2, P2O5 e MnO.
 - Modelo B - Óxidos + elementos traços: SiO2, Al2O3, Fe2O3, MgO, CaO, Na2O, K2O, TiO2, P2O5, MnO, Rb, Ba, Sr, Zr, Y e Nb.
 - Modelo C - Óxidos + elementos traços + 1 ETR: SiO2, Al2O3, Fe2O3, MgO, CaO, Na2O, K2O, TiO2, P2O5, MnO, Rb, Ba, Sr, Zr, Y, Nb e La.

Foram gerados três modelos distintos, pois nem todas as análises litogeoquímicas contém todos os elementos, devido ao alto custo. Por isso a idéia é que o usuário possa escolher o classificador que melhor se adeque aos dados do usuário.

## 2.3. Métricas de avaliação dos modelos 

### 2.3.1. Modelo A

 - **Acurácia da classificação:** 0,8911
 - **Erro da classificação:** 0,1089
 - **Precisão:** 0,8679
 - **Recall:** 0,9200
 - **ROC AUC:** 0,8923
 
### 2.3.2. Modelo B

 - **Acurácia da classificação:** 0,9307
 - **Erro da classificação:** 0,0693
 - **Precisão:** 0,9057
 - **Recall:** 0,9600
 - **ROC AUC:** 0,9320
 
### 2.3.3. Modelo C

 - **Acurácia da classificação:** 0,9604
 - **Erro da classificação:** 0,0396
 - **Precisão:** 0,9434
 - **Recall:** 0,9804
 - **ROC AUC:** 0,9613


# Comentários

 - As métricas de avaliação demonstram que o melhor modelo é o Modelo C, que abrange todos os óxidos, alguns elementos traços e um elemento terra rara (La);
 - Mesmo o Modelo A, que apresentou os piores resultados, demonstra grande capacidade para classificação de granitos;
 - Algum erro é esperado na classificação dos granitos, uma vez que, quanto mais evoluído for o magma, mais semelhanças os dois tipos de granitos apresentam;
 - Na inferência realizada, apenas uma amostra foi classificada incorretamente. Todas as amostras utilizadas para inferência são de granitos tipo I, contudo, uma foi classificada como tipo S. Esse erro não prejudica a análise, pois todas as análises são da mesma unidade, por isso, o usuário pode ignorar as amostras classificadas erroneamente com erros tão baixos.
