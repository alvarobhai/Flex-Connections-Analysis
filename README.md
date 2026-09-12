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

## Updated connection firmness methodology
The dashboard now treats the five rows (50%, 80%, 90%, 95%, 100%) as **Connection Capacity Firmness** levels, rather than percentages of constraint events addressed.

For a requested connection of `P` MW:
- Equivalent Connection Capacity = `P × firmness`.
- For each hour, required flexibility to make that equivalent capacity firm is `max(0, equivalent connection capacity − available network headroom)`.
- Required Flex (MW) is the maximum hourly shortfall.
- Flex-Dependent Hours (% of Year) is the share of hours where the hourly shortfall is greater than zero.
- DSR is applied first up to the available economic DSR capacity for the selected load type; BTM Flex is the residual requirement.

This separates the contractual/connection-capacity concept of firmness from the frequency with which flexibility is called upon.
