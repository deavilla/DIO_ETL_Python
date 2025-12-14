# DIO_ETL_Python
Projeto de ETL com Python para estudos no curso do Santander 2025 - Ciência de Dados com Python

# 📊 Projeto: Classificação de Engajamento de Usuários

## 🎯 1. Visão Geral e Objetivo

Este projeto demonstra a implementação completa de um pipeline **Extract, Transform, Load (ETL)** usando a linguagem **Python**. O objetivo central é transformar dados brutos de login em **informação estratégica** ao aplicar uma lógica de classificação para identificar o risco de abandono (*Churn*) de usuários.

### Metodologia do Pipeline 

| FASE | FERRAMENTA PRINCIPAL | AÇÃO |
| :---: | :---: | :--- |
| **E**xtract | Pandas (Leitura de Excel) | Coletar 20 registros de usuários, incluindo IDs, Nomes e Datas de Login de uma fonte simulada. |
| **T**ransform | Python + Pandas | Calcular dias de inatividade e aplicar um modelo de regras para classificação de risco (IA Simulada). |
| **L**oad | Pandas (`to_excel`) | Persistir o conjunto de dados enriquecido em um novo arquivo Excel. |

---

## 🛠️ 2. Detalhamento da Transformação (Modelo de Risco)

A etapa de Transformação (T) utiliza capacidades de processamento de dados para gerar novas colunas que agregam valor ao negócio. A transformação implementada foi a **Classificação de Engajamento do Usuário** (Opção 1).

### A. Métrica Base: Dias Inativos

Calculamos o tempo que cada usuário permaneceu inativo até uma data de referência fixa (14/12/2025).

$$Dias\ Inativos = Data\ de\ Referência - Último\ Login$$

### B. Lógica de Classificação de Risco (Modelo Simulado)

A lógica de classificação é um conjunto de regras (simulando um modelo de IA de classificação) aplicado aos *Dias Inativos* para segmentar os usuários por `Nivel_Engajamento` e `Risco_Churn`.

| Dias Inativos ($D_{inativo}$) | Nível de Engajamento | Risco de Churn | Ação Estratégica Sugerida | 
| :---: | :---: | :---: | :---: |
| $D_{inativo} \leq 7$ dias | **Alto** | Baixo | Monitoramento Padrão |
| $7 < D_{inativo} \leq 30$ dias | **Médio** | Médio | Campanhas de Reengajamento Leve |
| $30 < D_{inativo} \leq 90$ dias | **Baixo** | Alto | Intervenção Urgente (Sucesso do Cliente) |
| $D_{inativo} > 90$ dias | **Inativo** | Crítico | Considerar como Churn, Tentativa de Recuperação |

---

## 📝 3. Tecnologias e Entregáveis

### 🅰. Ferramentas Utilizadas

O projeto foi inteiramente desenvolvido em **Python**, aproveitando as seguintes bibliotecas:

* **Python:** Linguagem de programação central para orquestração.
* **Pandas:** Biblioteca essencial para manipulação e análise de dados (DataFrames).
* **datetime:** Utilizado para cálculos e manipulação de datas e horas.
* **Openpyxl (via Pandas):** Necessário para a leitura e escrita de arquivos Excel.

### Estrutura do código Python
```
# Importações
import pandas as pd
from datetime import datetime

# --- 1. ETAPA E: EXTRAÇÃO (Geração dos Dados) ---
# Criação do DataFrame 'df_original'
# Salva df_original para 'dados_originais.xlsx'

# --- 2. ETAPA T: TRANSFORMAÇÃO ---
# Define a função 'classificar_engajamento' (lógica de regras)
# Calcula a coluna 'Dias_Inativo'
# Aplica a função de classificação para criar 'Nivel_Engajamento' e 'Risco_Churn'
# Limpeza e formatação de colunas

# --- 3. ETAPA L: CARGA ---
# Salva o DataFrame 'df_transformado' para 'dados_transformados_engajamento.xlsx'
```

### 🅱. Arquivos Gerados

O pipeline resulta na criação e atualização de três artefatos principais:

| Arquivo | Tipo | Conteúdo e Função |
| :--- | :--- | :--- |
| `etl_script.py` | Código Python | Contém o código fonte completo que executa as etapas E, T e L. |
| `dados_originais.xlsx` | Planilha Excel | A representação da fonte de dados inicial (Extração). |
| `dados_transformados_engajamento.xlsx` | Planilha Excel | O dataset final enriquecido, pronto para consumo analítico (Carga). |


O arquivo de saída (`dados_transformados_engajamento.xlsx`) inclui todas as colunas originais mais as novas colunas de valor agregado: **`Dias_Inativo`**, **`Nivel_Engajamento`**, e **`Risco_Churn`**.
