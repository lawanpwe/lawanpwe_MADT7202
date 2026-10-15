# Which transit hub can Thailand not afford to lose?

MADT 7202 Web and Social Network Analytics Management · Mid-term applied case
Paweena Lawan (Dao) · 6810424024

**Run the notebook in Colab:** https://colab.research.google.com/drive/1WOo4I_1XuAkZx0GXonI8g9ysdZ5dzNx5?usp=sharing

## The question
The product manager of a Thai tour operator selling Latin America and Caribbean trips decides which transit hubs need a backup route.
Ranking hubs by size is a simple count. The real question is which markets are lost when one hub goes, and that depends on whether another hub reaches the same market: a network-overlap question.

## Main result
| Hub | Routes (size) | Countries for which it is the only one-stop link |
|---|---|---|
| Istanbul | 226 | 0 |
| Beijing | 204 | 0 |
| Dubai | 187 | 0 |
| **Madrid** | **138** | **4** (Bolivia, Costa Rica, Guatemala, Uruguay) |
| Paris | 237 | 3 |
| Frankfurt | 225 | 3 |

15 countries depend on a single hub; 11 are in Latin America and the Caribbean. Rank correlation between hub size and dependency: 0.35.

## Repository contents
| File | What it is |
|---|---|
| `Thailand_Hub_Dependency_Midterm.ipynb` | Full analysis, with outputs. Runtime → Run all reproduces every number in the report. |
| `fig_hub_dependency.png` | The figure used in the report (saved by the notebook). |
| `6810424024_Paweena_Lawan_Midterm.pdf` | The one-page report. |
| `verification_2026.csv` | Second source: the 8 only-link hubs checked by hand on Google Flights (nonstop filter) on 3 Oct 2026. |

## Data and permission
- **OpenFlights** `routes.dat` and `airports.dat`, downloaded by the notebook from https://github.com/jpatokal/openflights. Snapshot June 2014, 67,663 route records.
- **Licence:** Open Database License (ODbL). Attribution: OpenFlights.org. The raw files are not copied into this repository; the notebook downloads them.
- **Basemap:** Natural Earth (public domain).
- **No personal data** is used.

## Method in short
- Node = airport. Directed edge = at least one airline flies nonstop A to B (codeshares not counted). Unweighted: the question is whether a link exists, and the data has no frequency.
- Hubs = the 116 airports abroad that Thailand flies to nonstop. Targets = the 106 countries that need one stop.
- Left out of ranking: Thailand, countries with a Thai nonstop (e.g. Japan, China), countries with fewer than 10 outgoing routes.
- Country level, not airport level: by airport, Istanbul (34) and Manila (28) lead only because of their own domestic airports.
- Robustness (only-link countries, Madrid / Paris / Frankfurt): cutoff 5: 4/5/3 · cutoff 10: 4/3/3 · cutoff 20: 3/0/3 · with codeshares: 4/3/3.

## Limitations
- Route data is from 2014. Only the first leg (Thailand to hub) was re-checked for 2026; second legs (hub to market) are 2014 data.
- No seats, frequency or transfer times. A connection is not capacity.
