# Tab 4: Demand Comparison

36104 Assignment 3, group app "AI Data Centre Expansion".
Group app: https://ai-data-centre-expansion.streamlit.app/

**Group question:** Is the rapid expansion of AI data centres justified by the actual demand for AI?

**Persona:** Dana Reyes, an energy policy analyst deciding whether her state should build grid capacity for data centres as permanent demand.

**This tab asks:** is actual AI use growing at the same pace as data centre construction?

Built by Aaron Sapkota. This repo runs Tab 4 on its own. The same `tab4_demand.py` plugs into the group app through its `render()` function.

## Run

```
pip install -r requirements.txt
streamlit run tab4_demand.py
```

## Data (kept exactly as downloaded)

| File | Source | What the tab uses |
|---|---|---|
| `data/monthly-spending-data-center-us.csv` | U.S. Census Bureau Value of Construction Put in Place, deflated by Our World in Data. https://ourworldindata.org/grapher/monthly-spending-data-center-us | Monthly US data centre construction spending, constant 2021 US$ |
| `data/National.xlsx` | U.S. Census Bureau, Business Trends and Outlook Survey. https://www.census.gov/hfp/btos/data_downloads | Share of firms using AI in the last two weeks (revised question, Nov 2025 on), standard errors, survey reference dates |
| `data/AI Core Questions.xlsx` | Same page, Historical Data, "AI Core Questions (Original)" | Share of firms using AI (original question, Sep 2023 to Sep 2025) |

## What the tab does

It compares US data centre construction spending with the share of US firms using AI, both indexed to 100 at the start of each comparison window. The Census Bureau changed its AI question in November 2025, so there are two windows (Sep 2023 to Sep 2025, and Nov 2025 onward) that are never joined. A second chart shows the monthly gap between the two indexes as bars above or below zero, each labelled with its value. Two sliders let the user pick the start and end month of each window, and the cards, both charts, the verdict and the trace recalculate.

## Processing

All processing happens in `tab4_demand.py`: two-week survey estimates are averaged into the month their reference period ends, then each series is indexed to 100 in the first month of each comparison window.
