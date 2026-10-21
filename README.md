# Ciência de Dados — 2025/2

Material da disciplina **Ciência de Dados** (Mestrado em Informática — UFES), semestre 2025/2, ministrada pelo prof. Giovanni Comarela.

O repositório reúne os notebooks das aulas, as listas de exercícios resolvidas, o trabalho prático e o projeto final.

## Estrutura

```
.
├── aulas/               # Notebooks das aulas
├── listas/              # Listas de exercícios resolvidas
├── trabalho_pratico/    # Agrupamento de jogos da Steam por descrição
├── projeto_final/       # Previsão de resultados na Fórmula 1
└── requirements.txt
```

### Aulas

| # | Notebook | Tema |
|---|----------|------|
| 01 | [aula_01_intro](aulas/aula_01_intro.ipynb) | Introdução e regras do jogo |
| 02 | [aula_02_intro2](aulas/aula_02_intro2.ipynb) | Probabilidade |
| 03 | [aula_03_pandas](aulas/aula_03_pandas.ipynb) | Manipulação de dados com pandas |
| 04 | [aula_04_seaborn](aulas/aula_04_seaborn.ipynb) | Visualização básica de dados |
| 06 | [aula_06_webscraping](aulas/aula_06_webscraping.ipynb) | Obtenção de dados na web |
| 06 | [aula_06_webscraping_APIs](aulas/aula_06_webscraping_APIs.ipynb) | APIs |
| 07 | [aula_07_tfidf](aulas/aula_07_tfidf.ipynb) | Representação de dados textuais (TF-IDF) |
| 08 | [aula_08_metricas](aulas/aula_08_metricas.ipynb) | Dissimilaridades e métricas |
| 09 | [aula_09_dimensionalidade](aulas/aula_09_dimensionalidade.ipynb) | Maldição da dimensionalidade |
| 11 | [aula_11_algebra](aulas/aula_11_algebra.ipynb) | Revisão de álgebra linear |
| 12 | [aula_12_pca](aulas/aula_12_pca.ipynb) | PCA |
| 13 | [aula_13_svd](aulas/aula_13_svd.ipynb), [aula_13_svd2](aulas/aula_13_svd2.ipynb) | SVD |
| 14 | [aula_14_kmeans](aulas/aula_14_kmeans.ipynb) | Agrupamento e k-means |
| 15 | [aula_15_hierarquico](aulas/aula_15_hierarquico.ipynb) | Agrupamento hierárquico |
| 16 | [aula_16_spectral](aulas/aula_16_spectral.ipynb) | Agrupamento espectral |
| 17 | [aula_17_avaliacao_clusters](aulas/aula_17_avaliacao_clusters.ipynb) | Avaliação de agrupamentos |
| 18 | [aula_18_dbscan](aulas/aula_18_dbscan.ipynb) | DBSCAN |
| 19 | [aula_19_classificacao](aulas/aula_19_classificacao.ipynb) | Classificação |
| 21 | [aula_21_regressao_logistica](aulas/aula_21_regressao_logistica.ipynb) | Regressão logística |
| 22 | [aula_22_avaliacao_classificadores](aulas/aula_22_avaliacao_classificadores.ipynb) | Avaliação de classificadores |

### Listas

| Lista | Tema |
|-------|------|
| [lista_01](listas/lista_01.ipynb) | CDFs, boxplots e histogramas |
| [lista_02](listas/lista_02.ipynb) | Dissimilaridades e métricas |
| [lista_03](listas/lista_03.ipynb) | PCA, SVD e redução de dimensionalidade |

## Trabalho prático — Jogos da Steam

[Enunciado](trabalho_pratico/especificacao.ipynb) · [Solução](trabalho_pratico/trabalho_pratico.ipynb)

O trabalho investiga se a descrição de um jogo da Steam tem relação com os gêneros a que ele pertence, usando apenas aprendizado não supervisionado.

- **Pipeline:** pré-processamento do texto, TF-IDF, redução com TruncatedSVD (200 componentes, cerca de 20% da variância), visualização com t-SNE e agrupamento com K-Means (k = 20) e Spectral Clustering.
- **Resultados:** os grupos se sobrepõem bastante (silhueta máxima perto de 0,06). Mesmo assim, o K-Means encontrou temas semânticos claros, como corrida e *survival horror*. Rótulos como "Indie", "Action" e "Casual" aparecem espalhados por quase todos os grupos porque indicam o escopo do jogo e não o seu conteúdo.

## Projeto final — Fórmula 1

[Enunciado](projeto_final/especificacao.ipynb) · [Solução](projeto_final/projeto_final.ipynb)

O projeto prevê em qual faixa de classificação final um piloto vai terminar, a partir de dados disponíveis antes da corrida. As faixas são Vencedor (P1), Pódio (P2–P3), Pontos (P4–P10) e Sem pontos (P11+).

- **Dados:** Ergast Developer API, restritos à era híbrida (2014 em diante) na etapa de modelagem.
- **Análise exploratória:** vitórias por piloto e por equipe, confiabilidade, pit stops, ultrapassagens por circuito e conversão de pole position.
- **Agrupamentos:** perfis de pilotos, de circuitos e de construtores, com K-Means e agrupamento hierárquico.
- **Modelos:**

  | Modelo | Acurácia | Acurácia balanceada |
  |--------|----------|---------------------|
  | Random Forest | 75,34% | 73,45% |
  | XGBoost | 77,43% | 71,55% |

## Como executar

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

### Dados

Os arquivos de dados (`.csv`, `.parquet`) **não são versionados** (veja o `.gitignore`). Para reexecutar os notebooks, coloque os arquivos nos caminhos que eles esperam:

- **Trabalho prático:** `trabalho_pratico/steam_games.parquet`, gerado a partir de datasets públicos da Steam no Kaggle.
- **Projeto final:** `projeto_final/data/`, com os CSVs do Ergast (`circuits.csv`, `results.csv`, `races.csv`, `qualifying.csv`, `pit_stops.csv` etc.) e o arquivo `lap_times.parquet`.
- **Aulas e listas:** alguns notebooks baixam os dados direto da internet. Outros esperam arquivos locais, por exemplo `datasets-minicurso/abilene_traffic.csv` nas aulas de SVD e `dados_questao_4.csv` e `dados_questao_5.csv` na lista 1.

> A aula 11 importa os módulos auxiliares `laUtilities` e `demoUtilities`, que não estão neste repositório.

## Autor

Gabriel Falcone da Silva — Mestrado em Informática, UFES
