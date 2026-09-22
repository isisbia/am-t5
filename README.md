# 🏫 Pipeline de Análise e Preparação de Dados - Censo Escolar 2025

Este repositório contém o pipeline de Análise de Dados (AD) e Ciência de Dados (CD) desenvolvido sobre a base oficial do **Censo Escolar 2025 (INEP/MEC)**. O objetivo principal é tratar, pré-processar e exportar os dados em formatos otimizados para treino de algoritmos de **Redes Neurais**.

---

## 📌 Objetivos do Projeto

Conforme os requisitos da atividade, o projeto cumpre quatro etapas fundamentais:

1. **Análise de Dados & Extração de Categóricos:** Mapeamento da estrutura do dataset, contagem de registos, verificação de tipos de dados (numéricos e textuais/categóricos) e análise exploratória visual.
2. **Definição de Target Viável:** Identificação de um alvo preditivo binário ideal para aprendizado supervisionado em redes neurais.
3. **Limpeza e Pré-processamento (AD/CD):** Tratamento de valores nulos, remoção de colunas irrelevantes ou de alta cardinalidade e codificação de variáveis categóricas via *One-Hot Encoding*.
4. **Extração de Dados em Formato BIN e PKL:** Exportação do dataset final limpo nos formatos `.pkl` (metadados e estrutura Pandas) e `.bin` (matrizes binárias de alto desempenho).

---

## 📊 1. Análise Exploratória e Target Escolhido

* **Volume de Dados:** ~214.192 escolas registadas e 290 atributos de infraestrutura e localização.
* **Variáveis:** 278 colunas numéricas e 12 variáveis categóricas/texto.
* **Target Preditivo Escolhido:** `IN_LABORATORIO_INFORMATICA`
  * **Tipo:** Classificação Binária (`0` = Não possui laboratório de informática, `1` = Possui laboratório).
  * **Justificativa:** É uma variável de alto impacto para políticas públicas de inclusão digital e apresenta uma distribuição consistente para treinamento de redes neurais.

---

## 🧹 2. Técnicas de Limpeza Aplicadas (AD e CD)

Para evitar estouro de memória RAM durante o treinamento e prevenir *overfitting*:
* **Filtragem de Nulos:** Remoção de registos com o target ausente e eliminação de colunas com mais de 50% de dados faltantes.
* **Descarte de Altíssima Cardinalidade:** Remoção de nomes, códigos únicos de entidade e identificadores geográficos detalhados (ex: `NO_ENTIDADE`, `NO_MUNICIPIO`, `NU_CNPJ_ESCOLA_PRIVADA`).
* **Imputação de Dados:** Preenchimento de valores nulos em colunas numéricas com a mediana.
* **Encoding Leve:** Aplicação de *One-Hot Encoding* (`pd.get_dummies`) com otimização de tipos de dados (`int8` e `float32`).

---

## 📁 3. Ficheiros Gerados (Outputs)

Após o pré-processamento, são gerados três ficheiros principais:

* `dataset_processado.pkl`: Dicionário contendo os DataFrames originais `X` e `y` e a lista com o nome de todas as *features*.
* `X_data.bin`: Matriz das variáveis preditoras convertida em array de bytes (`float32`).
* `y_data.bin`: Vetor do target convertido em array de bytes (`int32`).

estação de carregamento direto para matrizes NumPy e bibliotecas de Deep Learning (**PyTorch** / **TensorFlow**).

---

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python 3.x
* **Ambiente:** Google Colab / Google Drive
* **Bibliotecas Principais:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `pickle`

---
