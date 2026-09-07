# high-value-decibels

Research question: near the decode threshold of a weak-signal digital mode
(WSPR, FT8, ...), is an additional decibel of signal worth more than a
decibel gained when the signal is already strong?

`analyze_wspr.py` looks at WSPR transmitters that used multiple power
levels and compares how many unique receiving stations heard them at each
level. It computes receiver growth per dB, `G = ln(receiver_ratio) / Δpower`,
and buckets the result by starting SNR (fine-grained bins and a
Weak/Medium/Strong three-region split), with bootstrap confidence intervals
on the three-region result.

`make_article_figures.py` renders the polished figures and summary table in
`output/article_figures/` from that analysis, used in the accompanying
article `HIgh Value dB QST.docx`.

## Data

Reads the same raw WSPR parquet files (10m/20m/40m, `data/WSPR <band>/WSPR
<band>/*.parquet`) as the [hf-propagation](https://github.com/tgilton/hf-propagation)
project, but this is a **separate research question** from that project's
propagation/solar-geometry work — it only cares about power level vs.
receiver count, not path geometry, SZA, or magnetic latitude. `data/` is
gitignored; point it at the same raw WSPR data directory to reproduce.

## Running

```
python analyze_wspr.py          # writes output/*.csv and output/*.png
python make_article_figures.py  # writes output/article_figures/
```
