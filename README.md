# concert-tours-cleaning

Cleaning a web-scraped table of the 20 highest-grossing concert tours by women with Python and pandas.

The raw table comes from Wikipedia and has typical scraping problems: money stored as text, footnote markers inside values, hidden non-breaking spaces in column names and year ranges stored as text. The notebook turns it into a clean, analysis-ready CSV file.

## Data cleaning steps

| Problem in raw data | Example | Fix |
| --- | --- | --- |
| Hidden non-breaking spaces in column names | `'actual\xa0gross'` | Lowercase names, replace `\xa0` with a normal space |
| Money values stored as text | `$780,000,000` | Remove `$` and `,`, convert to numbers |
| Footnotes inside values | `$229,100,000[b]`, `7[2]` | Remove `[...]` before converting |
| Table symbols in tour titles | `Sticky & Sweet Tour ‡[4][a]` | Remove `†`, `‡`, `*` and footnotes |
| Year range stored as text | `2008–2009` | New column `start_year` |
| Missing ranking values | `peak`: 11 of 20 missing | Kept as missing (not listed in that ranking) |
| Source reference column | `[15][16]` | Dropped |

## Checks and findings

- **Consistency:** `average gross` matches `actual gross / shows` for all tours within 1 dollar, except Lady Gaga's *The Monster Ball Tour* (difference of about 1,970 dollars per show).
- **Outliers (IQR method):** *The Eras Tour* and the *Renaissance World Tour* earn far more per show than the other tours. They are real values, so they stay in the data.
- **Duplicates:** no duplicate rows and no spelling variants of artist names.

## Files

```
concert-tours-cleaning/
├── concert_tours_cleaning.ipynb   # cleaning notebook
├── data/
│   ├── concert_tours_raw.csv      # raw table
│   └── concert_tours_clean.csv    # cleaned result
└── requirements.txt
```

## How to run

```
git clone https://github.com/mina-motaghinasab/concert-tours-cleaning.git
cd concert-tours-cleaning
pip install -r requirements.txt
jupyter notebook concert_tours_cleaning.ipynb
```

## Data source

[List of highest-grossing concert tours by women](https://en.wikipedia.org/wiki/List_of_highest-grossing_concert_tours_by_women), Wikipedia. Text and data are available under the [Creative Commons Attribution-ShareAlike 4.0](https://creativecommons.org/licenses/by-sa/4.0/) license. The files in `data/` are a copy of that table and are shared under the same license.

## Use of AI tools

I wrote the original cleaning code myself. I used Claude (an AI assistant) to review the notebook, reorganise it into clear sections with explanations and write this README. Claude also suggested three additions: removing footnotes before converting money values, cleaning the tour titles and saving the cleaned file. I can explain every step of the code.

## Author

Mina Motaghinasab, M.Sc. Data Science student at TU Dortmund
