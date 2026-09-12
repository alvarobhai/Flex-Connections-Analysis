# Flexible Connection Capacity Explorer — V2

Static GitHub Pages dashboard for screening how much connection capacity a constrained network can support when a customer can provide flexibility.

## Package
- `index.html` — dashboard application
- `data/model.json` — V6 hourly headroom profiles
- `data/flexible_connection_model_v6_firmness_thresholds_final.csv` — central-case outputs for the five connection firmness levels
- `data/flexible_connection_model_v6_DSR_portfolios_inspection.csv` — DSR portfolio inspection data
- `data/dsr_economic_capacity_by_segment.csv` and `data/dsr_economic_merit_order.csv` — economic DSR inputs
- `data/data_centre_dsr_v6_assumptions.csv` — data-centre DSR assumptions

## Connection firmness methodology
The dashboard models five **Connection Capacity Firmness** levels: 50%, 80%, 90%, 95% and 100%. These are no longer percentages of constraint events addressed.

For a requested connection of `P` MW and firmness `F`: 
1. **Equivalent Connection Capacity** = `P × F`.
2. For each hour, compare the equivalent connection capacity with the available network headroom.
3. **Hourly flexibility requirement** = `max(0, Equivalent Connection Capacity − Available Headroom)`.
4. **Required Flex (MW)** is the maximum hourly shortfall.
5. **Flex-Dependent Hours (% of Year)** is the share of hours where the hourly shortfall is greater than zero.
6. Available economic **DSR** is applied first; **BTM Flex** is the residual flexibility requirement.

This explicitly separates the connection-capacity firmness level from how often flexibility is required.

## Load types and DSR
- **Data Centres:** central economic DSR = 15% of peak load, comprising cooling/thermal, auxiliary systems and IT workload shifting.
- **Industrial & Manufacturing:** economic DSR uses the CLF-derived industrial segment merit order, with the closest-match `Other Industrial & Process Loads` portfolio in the dashboard.
- **Large Commercial / Mixed-use:** economic DSR uses the CLF `Offices & Business Services` end-use portfolio rather than a generic commercial label.

DSR is applied in merit order up to the available economic capacity; BTM Flex fills any residual requirement.

## Heatmap
The heatmap shows **Non-Firm Capacity (% of Requested Load)** by hour and day. It uses the selected customer load profile, so the non-firm share varies with both hourly customer demand and network headroom.

## Display conventions
- MW values above 10 MW are rounded to the nearest MW.
- Smaller MW values retain one decimal place.
- DSR and BTM Flex table headers are highlighted and include hover definitions.
- Table column headers include hover definitions explaining the model terms.
- The headline cards focus on the 90% firmness proposition, with a secondary 100% firmness benchmark.

## Design reference
The visual language follows the supplied GB Industrial & Commercial Flexibility Explorer: light grey/white canvas, compact left-hand controls, restrained typography, thin borders, KPI cards, and chart-led results.

## Deployment
Upload the contents of this folder to a GitHub repository with GitHub Pages enabled. No build step or server is required.


### Static hosting
The dashboard embeds the model data in `index.html` so it works reliably on GitHub Pages and other static hosts where relative JSON fetches can fail. The source `data/model.json` is retained in the repository for transparency and reuse.
