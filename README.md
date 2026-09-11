# Flexible Connection Capacity Explorer — V1

Static GitHub Pages dashboard for screening how much additional connection capacity a constrained network can support when a customer can provide flexibility.

## Package
- `index.html` — dashboard application
- `data/model.json` — V6 central-case headroom, firmness thresholds, DSR portfolio and data-centre assumptions

## Model logic
**Network capacity + customer load profile → hourly constraint → flexibility requirement → connection firmness.**

Three headroom scenarios are shown simultaneously:
1. High Year-Round Headroom + Short Summer Constraints
2. Variable Headroom + Summer Constraints
3. Lower & More Persistent Summer Headroom

The central data-centre DSR case is 15% of a 250 MW customer: 7.5 MW cooling/thermal, 5 MW auxiliary systems and 25 MW IT workload shifting. The illustrative costs are £200/MWh, £225/MWh and £250/MWh respectively.

DSR duration is 3 hours, with recovery assumptions of 4h cooling, 2h auxiliary and 8h IT workload. Solar is represented as coincident generation; storage is retained as a simple option and becomes relevant if solar/storage assumptions are extended.

## Design reference
The visual language intentionally follows the supplied GB Industrial & Commercial Flexibility Explorer: light grey/white canvas, compact left-hand controls, restrained typography, thin borders, KPI cards, and chart-led results.

## Deployment
Upload the contents of this folder to a GitHub repository with GitHub Pages enabled. No build step or server is required.
