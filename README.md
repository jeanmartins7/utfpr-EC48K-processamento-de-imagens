# Projeto Final: Classificação de Grãos de Café

**Processamento de Imagens**

## Equipe

* Jean Marcel Peres Martins

## Resumo do Projeto

Este projeto tem como objetivo aplicar técnicas de classificação de imagens utilizando a abordagem clássica de extração 
de características combinada com classificadores tradicionais. Focamos na classificação de diferentes tipos de grãos de café, 
utilizando o **Coffee Bean Dataset (224x224)**. O trabalho envolveu a extração de características de forma utilizando os 
Hu Moments, um processo de pré-processamento robusto e a otimização de um classificador Support Vector Machine (SVM) 
para alcançar os melhores resultados possíveis. O objetivo é compreender, comparar e avaliar o desempenho 
de diferentes estratégias.

## Metodologia

A metodologia aplicada seguiu a **Abordagem Clássica (Extração de Características + Classificação)**, conforme as diretrizes do projeto.

### Pré-processamento de Imagens

1.  **Carregamento e Redimensionamento:** Imagens coloridas do dataset foram carregadas e redimensionadas para 224x224 pixels.
2.  **Conversão para Escala de Cinza:** As imagens foram convertidas para escala de cinza, um passo essencial para a aplicação de técnicas de limiarização e extração de momentos.
3.  **Limiarização (Otsu):** A técnica de limiarização de Otsu foi aplicada para binarizar as imagens, isolando os grãos
de café do fundo. Esta etapa é crucial para a extração de características de forma.
4.  **Operações Morfológicas:** Após a limiarização, foram aplicadas operações morfológicas (abertura e fechamento) 
para remover ruídos e refinar a forma dos objetos binarizados, garantindo uma representação mais precisa para a extração de características.

### Descritor Implementado: Hu Moments

Os **Hu Moments** foram utilizados como método de extração de características. Este é um conjunto de sete momentos invariantes 
derivados dos momentos centrais de imagem. Eles são particularmente úteis para descrever a forma de um objeto em uma imagem 
e são robustos a transformações como translação, escala e rotação. A transformação logarítmica foi aplicada aos Hu Moments 
para estabilizar seus valores, tornando-os mais adequados para a entrada do classificador.

### Classificador e Otimização

Foi utilizado um **Support Vector Machine (SVM)** como classificador. Para otimizar seu desempenho, as seguintes técnicas foram aplicadas:

1.  **Normalização das Características:** As características (Hu Moments) extraídas foram normalizadas usando `StandardScaler` 
para garantir que todas as características contribuam igualmente para o treinamento do modelo.
2.  **Otimização de Hiperparâmetros (GridSearchCV):** Uma busca em grade (`GridSearchCV`) foi realizada para encontrar a 
melhor combinação de hiperparâmetros (como `C`, `gamma` e `kernel`) para o SVM. Esta busca sistemática garante que o 
modelo utilize sua configuração mais eficiente para o dataset. Os melhores parâmetros encontrados foram `{'C': 100, 'gamma': 1, 'kernel': 'rbf'}`.
3.  **Balanceamento de Classes:** O parâmetro `class_weight='balanced'` foi configurado no SVM para mitigar os efeitos 
de um possível desbalanço entre as classes do dataset.

## Resultados Obtidos

As seguintes métricas de desempenho foram obtidas no conjunto de teste após a otimização do modelo:

* **Acurácia:** 0.4979 (aproximadamente 49.79%) 
* **Precisão (média ponderada):** 0.5040 
* **Recall (média ponderada):** 0.4979
* **F1-score (média ponderada):** 0.4971

**Matriz de Confusão:**


|                | Previsto: Dark | Previsto: Green | Previsto: Light | Previsto: Medium |
|----------------|:--------------:|:---------------:|:---------------:|:----------------:|
| **Dark**       |      70        |       7         |      24         |       19         |
| **Green**      |      17        |      56         |      28         |       19         |
| **Light**      |      28        |      20         |      49         |       23         |
| **Medium**     |      35        |      11         |      10         |       64         |



**Análise dos Resultados:**
A acurácia otimizada de aproximadamente 49.79% representa uma melhoria significativa em relação à acurácia inicial 
(aproximadamente 33.75% antes das otimizações). A matriz de confusão demonstra uma melhora notável na classificação da 
classe 'Light' (de 7 para 49 acertos), que era um ponto fraco inicial do modelo. O classificador ainda apresenta desafios 
em distinguir algumas classes (como as confusões entre 'Dark', 'Light' e 'Medium'), mas o uso combinado de pré-processamento
aprimorado, características de forma e otimização de hiperparâmetros do SVM elevou consideravelmente o desempenho do modelo.

## Repositório do Projeto

O projeto completo, incluindo o código-fonte (notebook Jupyter), e o vídeo de apresentação, estão armazenados no seguinte repositório de arquivos:

[**LINK DO SEU REPOSITÓRIO (Google Drive, [GitHub](https://github.com/jeanmartins7/utfpr-EC48K-processamento-de-imagens))**]

## Instruções de Uso (Opcional - Adapte conforme necessário)

Para replicar este projeto, siga os passos:

1.  **Download do Dataset:** Certifique-se de que o "Coffee Bean Dataset (224x224)" esteja disponível localmente ou no 
seu Google Drive. A estrutura esperada é uma pasta base (`coffe-beans`) contendo subpastas `train`, `test`, e dentro
delas as pastas para cada classe (`Dark`, `Green`, `Light`, `Roasted`) com as imagens.
2.  **Configuração do Ambiente:** Utilize o Google Colab com Python. As bibliotecas necessárias (OpenCV, Numpy, Pandas, 
Scikit-learn, Matplotlib, Seaborn, Pillow) serão instaladas automaticamente pelo script.
3.  **Caminho do Dataset:** Ajuste a variável `pasta_base` no início do notebook para o caminho correto do seu dataset.
4.  **Execução:** Execute todas as células do notebook em sequência. O script realizará o carregamento das imagens, 
pré-processamento, extração de características, divisão de dados, normalização, treinamento e otimização do SVM, e a avaliação do modelo.


## Referências Bibliográficas

* **Otsu, N.** (1979). "A thresholding method from gray-level histograms." *IEEE Transactions on Systems, Man, and Cybernetics*, 9(1), 62-66.
* **Hu, M. K.** (1962). "Visual Pattern Recognition by Moment Invariants." *IRE Transactions on Information Theory*, 8(2), 179-187.
* **Cortes, C., & Vapnik, V.** (1995). "Support-Vector Networks." *Machine Learning*, 20(3), 273-297.

**Recursos e Documentações Online:**

* **Documentação Oficial do OpenCV:** [https://docs.opencv.org/4.x/d9/df8/tutorial_root.html](https://docs.opencv.org/4.x/d9/df8/tutorial_root.html)
* **PyImageSearch:** [https://www.pyimagesearch.com/](https://www.pyimagesearch.com/) (Procure por tutoriais de Thresholding, Morphological Operations, Hu Moments).
* **Scikit-learn Documentation:** [https://scikit-learn.org/stable/](https://scikit-learn.org/stable/) (Procure por `preprocessing`, `svm`, `model_selection.GridSearchCV`).
* **StatQuest with Josh Starmer:** (Pesquise por vídeos sobre "Support Vector Machines" para uma excelente explicação visual).