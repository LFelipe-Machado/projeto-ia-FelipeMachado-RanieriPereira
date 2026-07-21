# Previsão da Nota Média de Filmes no TMDB

Projeto final da disciplina de Aprendizado de Máquina — Universidade Federal de Sergipe.

## Objetivo

Construir e comparar modelos de regressão capazes de prever a **nota média que um filme recebe no
TMDB** (`vote_average`), a partir de atributos como quantidade de votos, idioma original e data de
lançamento.

## Integrantes

- Luís Felipe Rocha Machado
- Ranieri Pereira Carvalho Filho

## Fonte dos dados

[The Movie Database (TMDB)](https://www.themoviedb.org/), via datasets públicos extraídos e
disponibilizados no Kaggle:
- `data/movie_data.csv` — base principal usada na modelagem (2000 filmes).
- `data/Top_rated_movies.csv` — segunda extração, mantida apenas para documentar um problema de
  qualidade de dados encontrado (ver seção 5.2 do notebook); **não é usada na modelagem** porque contém
  apenas 20 filmes únicos duplicados 500 vezes cada.

Os dados são carregados no notebook diretamente das URLs *raw* deste repositório, sem depender de
arquivos locais.

## Tipo da tarefa

**Regressão** — o atributo-alvo (`vote_average`, nota de 0 a 10) é numérico contínuo.

## Organização dos arquivos

```
.
├── README.md
├── projeto_final.ipynb      # notebook principal com todo o desenvolvimento
└── data/
    ├── movie_data.csv
    └── Top_rated_movies.csv
```

## Como abrir no Google Colab

Clique no link abaixo (ou abra o `projeto_final.ipynb` pelo GitHub e clique em "Open in Colab"):

`https://colab.research.google.com/github/<USUARIO>/<REPO>/blob/main/projeto_final.ipynb`

*(link a ser atualizado com o endereço definitivo do repositório)*

## Modelos utilizados

- Baseline (previsão pela média de `vote_average`)
- Regressão Linear
- Árvore de Decisão (Regressor, `max_depth=6`, `min_samples_leaf=10`)
- Random Forest (Regressor) — **modelo final**, com hiperparâmetros ajustados via `GridSearchCV`
  (`n_estimators=100`, `max_depth=6`, `min_samples_leaf=5`)

## Principais resultados

Comparação por validação cruzada (5-fold, apenas no conjunto de treino):

| Modelo | RMSE médio (CV) | MAE médio (CV) |
|---|---|---|
| Baseline (média) | 0,868 | 0,683 |
| Regressão Linear | 0,738 | 0,568 |
| Árvore de Decisão | 0,710 | 0,540 |
| **Random Forest** | **0,679** | **0,517** |

Avaliação final no conjunto de teste (usado uma única vez, com o Random Forest ajustado):

- **MAE:** 0,526
- **MSE:** 0,456
- **RMSE:** 0,675

O RMSE de teste ficou muito próximo do RMSE de validação cruzada, indicando boa generalização (sem
overfitting nem vazamento de dados). Os três modelos superam claramente o baseline, mas a diferença
entre eles é modesta — uma limitação relacionada à quantidade reduzida de atributos preditivos
disponíveis no dataset (ver discussão completa na seção 5.7 do notebook).

## Divisão das contribuições

Ranieri Filho=


Luis Felipe=

## Link do vídeo

_(a preencher)_

## Declaração de uso de ferramentas de Inteligência Artificial

- **Ferramenta utilizada:** Claude (Anthropic).
- **Finalidade:** apoio na estruturação do notebook, na análise exploratória dos dados, na redação dos
  textos interpretativos e na escrita de código para pré-processamento, modelagem e avaliação.
- **Parte do trabalho em que foi utilizada:** todas as seções do notebook (5.1 a 5.7), como assistente
  de desenvolvimento sob orientação e revisão constante dos integrantes.
- **Forma de verificação:** todo o código foi executado pelos integrantes, que revisaram as
  interpretações, validaram os resultados numéricos e gráficos gerados, e são capazes de explicar e
  justificar cada decisão técnica tomada, conforme exigido na apresentação em vídeo.
