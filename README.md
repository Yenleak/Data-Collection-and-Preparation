# Highest-Grossing Films: What Makes a Box-Office Hit?

SIS №1 — Data Collection & Preparation, Kazakh-British Technical University.
Team: Kassymbay Nazym (24B032147), Sailaukhan Yenglik (24B031989).

## Data sources
| Source | Method | Data |
|---|---|---|
| [Wikipedia: List of highest-grossing films](https://en.wikipedia.org/wiki/List_of_highest-grossing_films) | Web scraping (`requests` + `BeautifulSoup`, robots.txt checked) | Top-50 films of all time and the top film of every year: worldwide gross, year, budget |
| [TMDb API v3](https://developer.themoviedb.org/docs) | REST API (search + movie details) | Budget, revenue, genres, rating, votes, runtime, release date |

## Research questions
1. Does a bigger budget mean a bigger box office?
2. Do highly rated films earn more?
3. Which genres make the most money?
4. How did box office change over the decades?

## Pipeline
1. **Scrape** two Wikipedia tables (found by column names; rowspan/colspan resolved).
2. **Clean** money text (`T $2,257,906,828`, ranges), titles (`†` = still in cinemas) and data types; remove duplicates (203 rows → 183 films).
3. **API** — for every film: search by title + year, choose the best match, download the details.
4. **Clean** API data — TMDb uses `0` for an unknown budget/revenue, treated as missing.
5. **Merge** by title + year; check that Wikipedia gross and TMDb revenue agree (median difference 0.4%).
6. **Analyze** — descriptive statistics, Pearson/Spearman correlations, ROI, genres, decades.
7. **Visualize** — 6 figures (Matplotlib / Seaborn).

## Files
| File | Description |
|---|---|
| `SIS_Kassymbay_Sailaukhan_Highest_Grossing_Films.ipynb` | Notebook with all code, outputs and figures |
| `report_Kassymbay_Sailaukhan.pdf` | Report (2 pages): approach, results, key insights |
| `requirements.txt` | Python libraries |

## How to run
1. Get a free TMDb API key: https://www.themoviedb.org/settings/api
2. Save it in a file `tmdb_api_key.txt` next to the notebook (the file is in `.gitignore`, so it is never committed).
3. `pip install -r requirements.txt`, then open the notebook and run all cells.
