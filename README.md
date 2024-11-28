# Classificação de Tickets com IA

Este repositório contém o código e a documentação para a construção de uma API que simula um sistema de gerenciamento de tickets, com o objetivo de classificar tickets de problemas em categorias pré-definidas utilizando técnicas de processamento de linguagem natural (NLP) e aprendizado de máquina.

## Sumário

- [Objetivo](#objetivo)
- [Arquitetura da API](#arquitetura-da-api)
- [Processamento de Dados e Pré-processamento](#processamento-de-dados-e-pré-processamento)
- [Definição de Classes para Classificação](#definição-de-classes-para-classificação)
- [Modelos de IA](#modelos-de-ia)
- [Treinamento e Avaliação do Modelo](#treinamento-e-avaliação-do-modelo)
- [Prompt de Classificação de Tickets](#prompt-de-classificação-de-tickets)
- [Requisitos](#requisitos)
- [Como Executar](#como-executar)

## Objetivo

Este projeto tem como objetivo a construção de uma API que simula a gestão de tickets e a classificação automática de tickets com base na causa raiz do problema. Utilizando técnicas de Processamento de Linguagem Natural (PLN), o modelo de IA é treinado para classificar tickets em seis categorias predefinidas:

- **API**: Problemas relacionados a integrações externas ou chamadas de API.
- **Código Legado**: Erros decorrentes de código desatualizado ou não mantido.
- **Problemas de Desempenho**: Inclui gargalos ou ineficiências de desempenho.
- **Erro de Lógica**: Falhas na implementação de algoritmos ou na lógica de programação.
- **Erro de UI**: Erros na interface de usuário, como problemas visuais ou funcionais.
- **Falha em Testes**: Bugs não detectados em fases de teste, mas que afetam a produção.

## Arquitetura da API

A API simula um sistema de gerenciamento de tickets com endpoints que permitem:

- Visualizar todos os tickets.
- Consultar detalhes de um ticket específico.
- Criar novos tickets.

A estrutura da resposta da API é inspirada no formato da API do Jira, com dados como título, descrição, comentários, causa raiz e funcionalidade afetada.

### Endpoints da API

- **GET /tickets**: Retorna todos os tickets registrados.
- **GET /tickets/{id}**: Retorna os detalhes de um ticket específico, dado seu ID.
- **POST /tickets**: Cria um novo ticket.

## Processamento de Dados e Pré-processamento

O pré-processamento dos dados inclui a limpeza e transformação do texto utilizando técnicas de NLP para preparar os dados para o treinamento do modelo de IA.

### Passos do Pré-processamento

- **Remoção de Stopwords**: Remover palavras comuns que não contribuem para o significado semântico.
- **Normalização de Texto**: Converter o texto para minúsculas e remover caracteres especiais e números.
- **Tokenização**: Quebrar o texto em unidades menores, como palavras ou tokens.
- **TF-IDF**: Aplicar o método de TF-IDF para calcular a relevância de palavras em cada ticket.
- **Embeddings de Palavras**: Usar técnicas como Word2Vec ou DistilBERT para representar palavras em vetores de alta dimensão.

### Ferramentas e Bibliotecas Utilizadas

- **NLTK**: Para processamento de linguagem natural (tokenização, remoção de stopwords).
- **Scikit-learn**: Para implementação de TF-IDF.
- **Transformers (DistilBERT)**: Para geração de embeddings de palavras.

## Definição de Classes para Classificação

As categorias de classificação são definidas da seguinte maneira:

- **API**: Problemas com integrações ou chamadas externas.
- **Código Legado**: Problemas devido a código desatualizado ou não mantido.
- **Problemas de Desempenho**: Inclui gargalos ou ineficiências.
- **Erro de Lógica**: Erros de programação no algoritmo.
- **Erro de UI**: Problemas na interface do usuário.
- **Falha em Testes**: Erros não detectados antes da liberação do software.

## Modelos de IA

### DistilBERT

DistilBERT é uma versão compacta e eficiente do BERT, altamente eficaz para tarefas de processamento de linguagem natural, como classificação de texto.

- **Vantagens**: Bom desempenho e capacidade de entender contexto e semântica do texto.
- **Uso**: Ideal para tarefas complexas de análise de texto.

### Random Forest

Random Forest é um modelo baseado em árvores de decisão que pode ser usado, mas tende a ser menos preciso em tarefas de NLP comparado a modelos baseados em embeddings como DistilBERT.

**Recomendação**: Optar pelo DistilBERT devido à sua capacidade de entender o contexto semântico das palavras e seu desempenho superior em tarefas de NLP.

## Treinamento e Avaliação do Modelo

### Divisão dos Dados

Os dados são divididos em **80% para treinamento** e **20% para teste**.

### Etapas do Treinamento

1. **Pré-processamento**: Tokenização e normalização dos textos.
2. **Extração de Características**: Usar TF-IDF ou embeddings de palavras para transformar os textos em características numéricas.
3. **Treinamento**:
   - **DistilBERT**: Fine-tuning do modelo usando a biblioteca Transformers.
   - **Random Forest**: Treinamento usando TF-IDF ou contagem de palavras.

### Avaliação

O desempenho do modelo é avaliado usando as seguintes métricas:

- Acurácia
- Precisão
- Recall
- F1-Score

#### Exemplo de Avaliação:

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

accuracy = accuracy_score(test_data['labels'], predictions)
precision = precision_score(test_data['labels'], predictions, average='weighted')
recall = recall_score(test_data['labels'], predictions, average='weighted')
f1 = f1_score(test_data['labels'], predictions, average='weighted')

print(f"Acurácia: {accuracy}")
print(f"Precisão: {precision}")
print(f"Recall: {recall}")
print(f"F1-Score: {f1}")
