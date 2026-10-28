# Australian Trade 2016–2025: From Resource Exports to the Meat Industry Outlook

> A visual analytics project in **Excel** and **Tableau** that turns ten years of Australian Bureau of Statistics trade data into change points, a product-level dashboard, an 8-step storyboard and a 2030 export forecast for the meat industry.

**Tools:** Excel (formulas, derived datasets) · Tableau (relationships, calculated fields, dashboards, story, forecasting)
**Data:** ABS International Trade in Goods, annual, 2016–2025, A$ millions · 10 main categories (SITC 0–9) · 67 sub-categories
**Interactive version:** [View the dashboard on Tableau Public](https://public.tableau.com/views/BaoAnhNguyen_14686380_A3/Dashboard3)

![Meat industry dashboard](images/dashboard.png)

---

## Key findings

- **Trade doubled, structure didn't.** Exports rose from $258bn to $523bn (×2.0) and imports from $254bn to $461bn (×1.8). Australia is still a resource exporter and a manufactured-goods importer.
- **Resources dominate exports.** Crude materials (34.5%) and mineral fuels (26.8%) made up 61% of exports in 2025.
- **Machinery dominates imports.** Machinery and transport equipment held 40–41% of imports every year, reaching $191bn in 2025.
- **Three economy-wide change points:** the 2020 COVID-19 shock, the 2021 iron-ore boom, and the 2022 energy-price spike, when mineral-fuel exports rose 99% in one year to $251bn.
- **Meat is the backbone of food exports.** Meat exports grew from $11.1bn to $27.2bn (×2.45, CAGR 10.5%), lifting meat's share of food exports from 34% to 44%, with a $26.0bn trade surplus in 2025.
- **Meat is far more stable than cereals.** Coefficient of variation: cereals 47% vs meat 29%, because harvests depend on rainfall.
- **2030 outlook:** Tableau forecasts $33.0bn, against a recommended 5% annual growth target of $34.7bn.

---

## The question

Who is this for? Policy and government readers who need to see **where Australia's trade is growing, where it is exposed, and which industries deserve attention**.

The analysis moves from the whole economy down to one product:

```
Total trade  →  10 main categories  →  Food and live animals  →  Meat and meat preparations
                                                               (compared with Cereals)
```

Meat was chosen because it is Australia's largest agricultural export, shows clear change points, and depends on policy levers such as market access, biosecurity and supply chains. Cereals is the comparison because it is the second-largest food export and behaves very differently.

---

## Approach

### 1. Data preparation in Excel

Raw values range from under $1 million to over $250 billion, so dollar values alone hide how small categories behave. I built two derived datasets for both exports and imports:

| Pattern | Formula | Purpose |
|---|---|---|
| **Statistical (share)** | main category ÷ total; sub-category ÷ its main category | Compare categories of very different size |
| **Analytical (year-on-year ratio)** | value in year *t* ÷ value in year *t−1* (100% = no change) | Spot jumps and falls (change points) |

- A **check column** sums the ten main shares; it equals 100% in every year for both flows, which validates the formulas.
- Three cells divided by a zero base (export sub-categories 23 Crude rubber in 2018 and 96 Coin in 2019–2020). These were **left blank rather than reported as errors**.
- Exports and imports were stacked into three combined sheets (**Dollar**, **Statistical**, **Analytical**), each keyed on `Time` and `Trade` (Export/Import), with values pasted as values so no formula breaks in Tableau.

### 2. Data model in Tableau

The three combined sheets are linked through a **relationship on `Time` and `Trade`**, so a single view can show dollars, shares and growth for the same year and flow without duplicating rows.

### 3. Visualisation design

Each chart answers one question:

| Chart | Data pattern | Question it answers |
|---|---|---|
| Multi-line time series | Dollar | How did each category's value move over ten years? |
| Small multiples (export vs import) | Dollar | Where does Australia export more than it imports? |
| 100% stacked area | Statistical | Which categories dominate, and is the mix shifting? |
| Heatmap (diverging, centred on 100%) | Analytical | Was a change point broad-based or isolated? |
| Treemap + packed bubbles | Statistical / Dollar | How is Food split between sub-categories? |
| Growth bar with 0% reference line | Analytical | In which years did meat exports rise or fall? |
| Trade balance bar (calculated field) | Dollar | What did Australia gain from meat? |
| Forecast with 95% prediction band | Dollar | Where are meat exports heading by 2030? |

**Design rules applied throughout**
- Exports are always one colour and imports another; category colours stay the same across every sheet.
- Every chart has a title stating its scope and unit, and two to four annotations.
- Annotations follow the pattern **year + what happened + size + why**, e.g. *"2022 peak: $251bn (+99%) – energy crisis after the Russia–Ukraine war"*.

---

## Results

### Change points across the economy

![Year-on-year growth heatmap](images/heatmap.png)

| Year | Category | Change | Likely cause |
|---|---|---|---|
| 2020 | Mineral fuels | −30% | COVID-19 demand slump; China's informal restrictions on Australian coal |
| 2021 | Crude materials | +30% | Record iron-ore prices |
| 2021 | Beverages | −23% | China's anti-dumping tariffs on Australian wine |
| 2022 | Mineral fuels | +99% to $251bn | Energy crisis after Russia's invasion of Ukraine |
| 2022 | Total exports | +30% to $594bn | Broad commodity-price boom |
| 2024 | Beverages | +25% | China removed wine tariffs from March 2024 |
| 2025 | Commodities n.e.s. | +47% to $66.4bn | Record gold prices |

The trade surplus widened from $4.1bn in 2016 to a peak of $176.9bn in 2022, then narrowed to $62.2bn in 2025. **The surplus depends on resource prices, while the machinery deficit (−$168.7bn in 2025) is structural.**

### Inside Food: meat vs cereals

- **Meat** grew ×2.45 to $27.2bn; its share of food exports rose from 34.0% to 43.9%.
- **Cereals** grew ×2.13 to $16.2bn, but in steps: a $5.9bn drought low in 2019, a record $20.7bn in 2022, then −33% in 2024.
- Together, meat and cereals rose from **57% to 70% of food exports**, so food exports are becoming more concentrated.
- **Live animal exports** fell from $1.87bn to $1.30bn, so value is shifting from live animals to processed meat.

### Meat industry dashboard

![Meat dashboard](images/dashboard.png)

KPI tiles (2025 surplus, 10-year growth, 2025 exports) plus five linked panels:

- **A:** meat exports vs imports, with cereals for comparison
- **B:** meat share of Food
- **C:** year-on-year growth (green = rise, red = fall)
- **D:** trade balance, from the calculated field `SUM([Meat Export]) - SUM([Meat Import])`
- **E:** volatility (coefficient of variation), meat vs cereals

Meat exports fell in only **one year out of nine** (2020, −11%, COVID-19 and China's suspension of four beef plants).

### Storyboard: from the whole economy to one product

![Storyboard](images/storyboard.png)

Eight story points, each with a caption that states the finding:

1. Australia's goods trade doubled in ten years; the surplus peaked at $177bn in 2022
2. Exports: iron ore and energy set both the level and the shocks
3. Imports: machinery is 41% of imports and fuel exposure is rising
4. 2020 shrank most categories; 2022 lifted almost all of them
5. Inside Food: Australia exports meat and grain, imports coffee and processed food
6. Meat became 44% of food exports, and its surplus reached $26bn
7. Meat is the stable earner; cereals rise and fall with the rain
8. Meat exports to 2030: Tableau forecast, the target, and an AI forecast

### 2030 forecast

![Meat export forecast](images/forecast.png)

| Year | Linear trend | Tableau forecast | 5% target | Gap |
|---|---|---|---|---|
| 2026 | $24.3bn | $26.4bn (95%: $20.9–31.8bn) | $28.6bn | −$2.2bn |
| 2028 | $27.1bn | $29.7bn | $31.5bn | −$1.8bn |
| 2030 | $30.0bn | $33.0bn (95%: ~$25–41bn) | $34.7bn | −$1.7bn |

- Tableau used **exponential smoothing** (additive level and trend, no seasonality). Its quality metric is honest about the limits: **MAPE 15.7%, rated poor**, because ten annual points and the 2020 shock leave a wide band.
- **Why a 5% target:** the straight-line trend under-weights the 2024–25 surge, and repeating the 10.5% historic rate is too optimistic, because 2025 was lifted by cyclical factors (high cattle turn-off and a temporary US beef shortage). 5% sits above trend but inside the 95% band, so it is achievable, but only with active policy support.

### Tableau vs an AI assistant

I gave the same series to an AI assistant (Microsoft Copilot) and compared the outputs:

| | Tableau | AI assistant |
|---|---|---|
| 2030 forecast | $33.0bn (95% band ~$25–41bn) | $42.3bn (range $38.1–46.5bn) |
| Method | Exponential smoothing, with error metrics | Assumed growth rates (12% → 7%); no model fit |
| Repeatable | Yes | No; answers vary between runs |

Both agreed on the history and the change points, but the AI treated the 2024–25 surge as a new trend. **Verdict:** the AI is useful for context and hypotheses, but Tableau's forecast is the one to use for policy, because its method and uncertainty are visible and repeatable. Every AI claim used in the analysis was checked against ABS data or an external source.

---

## Recommendations for the meat industry

1. **Diversify markets:** the 2020 suspension of four beef plants cut $1.8bn of exports in one year.
2. **Invest in processing capacity and supply-chain resilience:** record turn-off in 2024–25 means growth now depends on abattoir, cold-chain and port capacity.
3. **Move up the value chain:** value is shifting from live animals to processed meat; premium, branded and chilled products raise the price per tonne.
4. **Manage biosecurity and climate risk:** a disease outbreak or major drought would hit herds and market access at once.

**Monitoring indicator:** exports below $28.6bn in 2026 or $30.0bn in 2027 should trigger a review.

---

## What I learned

- **Raw dollars hide the story.** Share and growth-ratio views exposed patterns that a $250bn category would otherwise drown out.
- **Dashboards explore; stories explain.** The dashboard suited analysts comparing several views at once; the storyboard suited decision-makers who need one finding per step.
- **A forecast is only as good as its uncertainty.** Showing the 95% band and the MAPE made the forecast more useful, not less.
- **AI is a second opinion, not a source.** It was fast and added context, but its figures needed checking and its forecast could not be audited.

---

## Repository contents

```
├── README.md
├── data/
│   └── australia_trade_2016_2025.xlsx   # raw ABS data + statistical/analytical patterns + combined sheets
├── tableau/
│   └── australia_trade.twbx             # packaged workbook (opens with data included)
└── images/                              # dashboard, storyboard and chart screenshots
```

**Excel workbook sheets:** `Export-dataset`, `Import-dataset`, `Export/Import statistical pattern`, `Export/Import analytical pattern`, `Dollar-combined`, `Statistical-Combined`, `Analytical-Combined`.

To open the workbook, use [Tableau Public](https://public.tableau.com/app/discover) (free) or Tableau Desktop.

---

## Data source

Australian Bureau of Statistics (2026). *International trade: Supplementary information, calendar year, 2025.* ABS data is licensed under [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/).
https://www.abs.gov.au/statistics/economy/international-trade/international-trade-supplementary-information-calendar-year/latest-release

Context for the change points: Reserve Bank of Australia, Meat & Livestock Australia, ABARES, World Gold Council, U.S. Energy Information Administration, World Bank, Beef Central, and Australian Government media releases (full list in the original report).

---

*Built by Bao Anh Nguyen · [LinkedIn](#) · [GitHub](#)*
