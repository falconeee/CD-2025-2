# Roteiro de Análise de Dados - Fórmula 1

Este documento descreve o plano inicial para a análise de dados do campeonato de Fórmula 1, aplicando técnicas de Ciência de Dados (Clusterização, Classificação e Regressão) conforme solicitado.

## 1. Definição do Problema
**Objetivo:** Analisar o histórico de corridas de Fórmula 1 para identificar padrões de desempenho de pilotos e construtores, e criar modelos preditivos para resultados de corridas.

## 2. Preparação dos Dados
O dataset consiste em vários arquivos CSV. O primeiro passo é consolidar essas informações.
*   **Arquivos Principais:**
    *   `results.csv`: Resultados detalhados (posição, pontos, voltas).
    *   `races.csv`: Informações de cada corrida (data, circuito, ano).
    *   `drivers.csv`: Informações dos pilotos.
    *   `constructors.csv`: Informações das equipes.
    *   `circuits.csv`: Dados geográficos e de altitude dos circuitos.
    *   `qualifying.csv`: Resultados de qualificação (importante para predição).
    *   `status.csv`: Razão de falha/término (importante para filtrar acidentes/problemas mecânicos).

*   **Ações de Limpeza:**
    *   Tratar valores nulos (representados como `\N` no CSV).
    *   Converter colunas de tempo (ex: "1:34:50.616") para milissegundos ou segundos.
    *   Categorizar variáveis categóricas (One-Hot Encoding para Equipes/Nacionalidade se necessário).
    *   Filtrar temporadas (ex: focar na "Era Híbrida" pós-2014 ou incluir tudo dependendo da análise).

## 3. Análise Exploratória (EDA)
Antes da modelagem, responder perguntas como:
*   Qual a correlação entre a posição de largada e a vitória?
*   Como a confiabilidade dos carros evoluiu ao longo dos anos (análise de `status.csv`)?
*   Quais circuitos favorecem ultrapassagens?

## 4. Modelagem e Algoritmos

### A. Clusterização (Não-Supervisionado)
**Ideia:** Agrupar pilotos por "Estilo de Pilotagem" ou "Desempenho".
*   **Features:** Média de pontos por corrida, desvio padrão de posições (consistência), número de voltas mais rápidas, taxa de abandono (DNF).
*   **Algoritmo:** K-Means ou DBSCAN.
*   **Esperado:** Grupos como "Lendas", "Consistentes", "Arriscados", "Novatos".
*   **Alternativa:** Agrupar circuitos por características de velocidade e vitória (circuitos onde a Pole Position é crucial vs. circuitos onde é menos importante).

### B. Classificação (Supervisionado)
**Ideia:** Prever se um piloto terminará no **Pódio (Top 3)** em uma determinada corrida.
*   **Target:** `positionOrder <= 3` (Binário: 1 ou 0).
*   **Features:**
    *   Posição de largada (`grid`).
    *   Pontos acumulados na temporada até aquele momento.
    *   Histórico do piloto/equipe no circuito específico.
    *   Idade do piloto.
*   **Algoritmos:** Random Forest, Logistic Regression, XGBoost.
*   **Métrica:** Acurácia, F1-Score, ROC-AUC.

### C. Regressão (Supervisionado)
**Ideia:** Prever a **quantidade de pontos** que um piloto fará na corrida.
*   **Target:** `points` (Note: o sistema de pontuação muda ao longo dos anos, considerar prever a `positionOrder` e converter, ou normalizar os pontos).
*   **Alternativa:** Prever o *tempo de volta* na qualificação.
*   **Features:** Similar à classificação + condições climáticas (se disponíveis), tempos de treino livre (se disponíveis na qualificação).
*   **Algoritmos:** Linear Regression, Gradient Boosting Regressor (XGBoost/LightGBM).
*   **Métrica:** RMSE (Root Mean Squared Error).

## 5. Cronograma Sugerido
1.  **Semana 1:** Leitura, limpeza e merge dos dados; Análise Exploratória Básica.
2.  **Semana 2:** Engenharia de Atributos (criar features como "vitórias passadas no circuito").
3.  **Semana 3:** Implementação e teste dos modelos de Classificação e Regressão.
4.  **Semana 4:** Implementação da Clusterização e refinamento dos modelos.
5.  **Semana 5:** Criação, documentação e vídeo final.
