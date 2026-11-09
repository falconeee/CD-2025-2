# Data Science — 2025/2

Material for the **Data Science** course (Master's in Computer Science — UFES), semester 2025/2, taught by Prof. Giovanni Comarela.

The repository gathers the lecture notebooks, the solved exercise lists, the hands-on assignment and the final project.

## Structure

```
.
├── aulas/               # Lecture notebooks
├── listas/              # Solved exercise lists
├── trabalho_pratico/    # Clustering Steam games by description
├── projeto_final/       # Predicting Formula 1 results
└── requirements.txt
```

### Lectures

| # | Notebook | Topic |
|---|----------|------|
| 01 | [aula_01_intro](aulas/aula_01_intro.ipynb) | Introduction and ground rules |
| 02 | [aula_02_intro2](aulas/aula_02_intro2.ipynb) | Probability |
| 03 | [aula_03_pandas](aulas/aula_03_pandas.ipynb) | Data manipulation with pandas |
| 04 | [aula_04_seaborn](aulas/aula_04_seaborn.ipynb) | Basic data visualization |
| 06 | [aula_06_webscraping](aulas/aula_06_webscraping.ipynb) | Getting data from the web |
| 06 | [aula_06_webscraping_APIs](aulas/aula_06_webscraping_APIs.ipynb) | APIs |
| 07 | [aula_07_tfidf](aulas/aula_07_tfidf.ipynb) | Representing text data (TF-IDF) |
| 08 | [aula_08_metricas](aulas/aula_08_metricas.ipynb) | Dissimilarities and metrics |
| 09 | [aula_09_dimensionalidade](aulas/aula_09_dimensionalidade.ipynb) | Curse of dimensionality |
| 11 | [aula_11_algebra](aulas/aula_11_algebra.ipynb) | Linear algebra review |
| 12 | [aula_12_pca](aulas/aula_12_pca.ipynb) | PCA |
| 13 | [aula_13_svd](aulas/aula_13_svd.ipynb), [aula_13_svd2](aulas/aula_13_svd2.ipynb) | SVD |
| 14 | [aula_14_kmeans](aulas/aula_14_kmeans.ipynb) | Clustering and k-means |
| 15 | [aula_15_hierarquico](aulas/aula_15_hierarquico.ipynb) | Hierarchical clustering |
| 16 | [aula_16_spectral](aulas/aula_16_spectral.ipynb) | Spectral clustering |
| 17 | [aula_17_avaliacao_clusters](aulas/aula_17_avaliacao_clusters.ipynb) | Cluster evaluation |
| 18 | [aula_18_dbscan](aulas/aula_18_dbscan.ipynb) | DBSCAN |
| 19 | [aula_19_classificacao](aulas/aula_19_classificacao.ipynb) | Classification |
| 21 | [aula_21_regressao_logistica](aulas/aula_21_regressao_logistica.ipynb) | Logistic regression |
| 22 | [aula_22_avaliacao_classificadores](aulas/aula_22_avaliacao_classificadores.ipynb) | Classifier evaluation |

### Exercise lists

| List | Topic |
|-------|------|
| [lista_01](listas/lista_01.ipynb) | CDFs, boxplots and histograms |
| [lista_02](listas/lista_02.ipynb) | Dissimilarities and metrics |
| [lista_03](listas/lista_03.ipynb) | PCA, SVD and dimensionality reduction |

## Hands-on assignment — Steam games

[Statement](trabalho_pratico/especificacao.ipynb) · [Solution](trabalho_pratico/trabalho_pratico.ipynb)

The assignment investigates whether a Steam game's description relates to the genres it belongs to, using unsupervised learning only.

- **Pipeline:** text preprocessing, TF-IDF, reduction with TruncatedSVD (200 components, about 20% of the variance), visualization with t-SNE and clustering with K-Means (k = 20) and Spectral Clustering.
- **Results:** the clusters overlap a lot (maximum silhouette around 0.06). Even so, K-Means found clear semantic themes, such as racing and *survival horror*. Labels such as "Indie", "Action" and "Casual" are spread across almost every cluster because they describe the game's scope, not its content.

## Final project — Formula 1

[Statement](projeto_final/especificacao.ipynb) · [Solution](projeto_final/projeto_final.ipynb)

The project predicts which final-position band a driver will finish in, from data available before the race. The bands are Winner (P1), Podium (P2–P3), Points (P4–P10) and No points (P11+).

- **Data:** Ergast Developer API, restricted to the hybrid era (2014 onwards) in the modeling stage.
- **Exploratory analysis:** wins by driver and by team, reliability, pit stops, overtakes per circuit and pole position conversion.
- **Clustering:** driver, circuit and constructor profiles, with K-Means and hierarchical clustering.
- **Models:**

  | Model | Accuracy | Balanced accuracy |
  |--------|----------|---------------------|
  | Random Forest | 75.34% | 73.45% |
  | XGBoost | 77.43% | 71.55% |

## How to run

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

### Data

The data files (`.csv`, `.parquet`) are **not versioned** (see `.gitignore`). To rerun the notebooks, place the files at the paths they expect:

- **Hands-on assignment:** `trabalho_pratico/steam_games.parquet`, built from public Steam datasets on Kaggle.
- **Final project:** `projeto_final/data/`, with the Ergast CSVs (`circuits.csv`, `results.csv`, `races.csv`, `qualifying.csv`, `pit_stops.csv`, etc.) and the file `lap_times.parquet`.
- **Lectures and lists:** some notebooks download their data straight from the internet. Others expect local files, for example `datasets-minicurso/abilene_traffic.csv` in the SVD lectures and `dados_questao_4.csv` and `dados_questao_5.csv` in list 1.

> Lecture 11 imports the helper modules `laUtilities` and `demoUtilities`, which are not in this repository.

## Author

Gabriel Falcone da Silva — Master's in Computer Science, UFES
