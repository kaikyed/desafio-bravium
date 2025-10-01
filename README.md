# Análise de Sentimentos de Avaliações de E-commerce Brasileiro

Este projeto apresenta um modelo de *Machine Learning* para análise de sentimentos, treinado com avaliações de consumidores de um grande e-commerce brasileiro. O objetivo é classificar automaticamente as avaliações escritas como **positivas** ou **negativas** com base no texto do comentário.

O código foi desenvolvido em um notebook Jupyter (`.ipynb`) e segue um fluxo estruturado, desde a importação dos dados até a exportação dos resultados.

## 📂 Estrutura do Projeto

O notebook está dividido nas seguintes seções:

### 1. Importação das Bibliotecas
Nesta seção, todas as bibliotecas necessárias para o projeto são importadas:
- **Pandas e NumPy:** para manipulação e análise de dados.
- **Matplotlib e Seaborn:** para visualização de gráficos.
- **Scikit-learn (sklearn):** para a construção do pipeline de *Machine Learning*, incluindo pré-processamento de texto, treinamento do modelo e avaliação de métricas.
- **NLTK (Natural Language Toolkit):** para processamento de linguagem natural (PLN), especificamente para a remoção de *stopwords* (palavras comuns sem valor semântico).

### 2. Carregamento e Análise Exploratória dos Dados (EDA)
Aqui, o conjunto de dados `olist_order_reviews_dataset.csv` é carregado. Uma análise exploratória inicial é realizada para:
- Visualizar as primeiras linhas e a estrutura do DataFrame.
- Verificar a distribuição das notas de avaliação (de 1 a 5 estrelas).
- Identificar e quantificar valores nulos, especialmente nos campos de comentários.

### 3. Engenharia de Features e Preparação do Dataset
Esta é uma etapa crucial para transformar os dados brutos em um formato adequado para o modelo:
- **Criação da Variável Alvo (`sentimento`):** Uma nova coluna é criada para classificar o sentimento com base na nota da avaliação.
  - **Positiva (1):** Avaliações com nota 4 ou 5.
  - **Negativa (0):** Avaliações com nota 1 ou 2.
- **Remoção de Dados Neutros:** Avaliações com nota 3 são consideradas neutras e foram removidas para criar um modelo de classificação binária mais claro e objetivo.
- **Limpeza de Dados:** Comentários nulos são descartados, pois são o foco da análise.

### 4. Pré-processamento, Treino e Avaliação do Modelo
Nesta seção, o modelo de *Machine Learning* é construído, treinado e avaliado:
- **Divisão dos Dados:** O dataset é dividido em conjuntos de treino (80%) e teste (20%).
- **Pipeline de Modelagem:** Um `Pipeline` do Scikit-learn é utilizado para automatizar o fluxo de trabalho. Ele consiste em duas etapas:
  1. **Vetorização com `TfidfVectorizer`:** O texto das avaliações é convertido em uma matriz numérica. Este processo remove *stopwords* em português, considera unigramas e bigramas (`ngram_range=(1, 2)`) e limita o vocabulário às 5.000 features mais relevantes para otimizar a performance.
  2. **Classificação com `LogisticRegression`:** Um modelo de Regressão Logística é treinado para classificar os sentimentos com base nos vetores de texto.
- **Avaliação de Performance:** O modelo treinado é avaliado com os dados de teste. São gerados:
  - **Relatório de Classificação:** Com métricas como precisão, recall e F1-score.
  - **Matriz de Confusão:** Para visualizar os acertos e erros do classificador.

### 5. Bônus: Extraindo os Motivos da Classificação
Para adicionar interpretabilidade ao modelo, esta seção extrai as palavras e termos (features) que mais influenciaram as decisões do classificador. Os coeficientes da Regressão Logística são analisados para identificar:
- **Termos mais positivos:** Palavras com altos coeficientes positivos.
- **Termos mais negativos:** Palavras com altos coeficientes negativos.

### 6. Exportando os Resultados
Finalmente, os resultados da análise são exportados para arquivos `.csv` em uma pasta de destino, facilitando a consulta e o compartilhamento:
1. **`relatorio_de_performance.csv`:** Contém as métricas de performance do modelo.
2. **`analise_palavras_influentes.csv`:** Lista as 50 palavras mais positivamente e negativamente influentes.
3. **`previsoes_no_conjunto_de_teste.csv`:** Mostra o texto original da avaliação, seu sentimento real e a previsão feita pelo modelo para cada item do conjunto de teste.

## 🚀 Como Executar
1. Certifique-se de ter o Python e as bibliotecas listadas na Seção 1 instaladas.
2. Faça o download do arquivo `olist_order_reviews_dataset.csv`.
3. Atualize a variável `caminho_do_arquivo` na Célula 2 com o caminho local do dataset.
4. Execute todas as células do notebook em ordem. Os resultados serão salvos na pasta especificada na Célula 6.
