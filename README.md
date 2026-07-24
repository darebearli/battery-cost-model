# LFP Battery Pack Should-Cost Reconstruction

A source-traceable reconstruction of Argonne National Laboratory's **2026
low-cost LFP, 75-kWh BEV pack scenario**, plus a simple component-price
sensitivity analysis.

This is a learning project for understanding cost drivers and procurement
tradeoffs. It is not a supplier quotation, a forecast of an executable market
price, or a full reimplementation of BatPaC.

## Base case

The defined Argonne scenario assumes:

- LFP cathode and 95% graphite / 5% silicon anode
- 125-Ah cells and 90-µm electrode thickness
- 50-GWh/year manufacturing scale
- 92% cell yield

The notebook reconstructs a pack cost of **$102.08/kWh**, versus Argonne's
published **$102.20/kWh**. The $0.12/kWh difference is caused by rounding in
the published component line items.

## What the model does

- Reconstructs material costs using Argonne component prices and published
  $/kWh contributions
- Preserves the correct mixed units: $/kg for active materials, $/m² for
  current collectors and separator, and $/L for electrolyte
- Reconstructs the full pack stack, including purchased items, BMS,
  conversion, overhead, R&D, financing, profit, and warranty
- Tests one-at-a-time ±30% price changes for the three largest selected
  component drivers

## Output

![Cost Breakdown](cost_breakdown.png)
![Sensitivity Analysis](sensitivity.png)

## Where the inputs come from

The primary source is Argonne National Laboratory,
[*Cost of Automotive Batteries for Electric Vehicles — Update
2024*](https://publications.anl.gov/anlpubs/2024/01/187177.pdf), report
ANL/CSE-24/1:

| Input | Location in source |
|---|---|
| Scenario definition | Table 10 |
| LFP and anode active-material prices | Table 11 |
| Electrolyte, separator, additives, binders, solvent, and current-collector prices | Table 12 |
| Complete 2026 pack-cost stack | Table 27 |
| Material $/kWh contributions | Table 28 |

The physical quantities shown in the notebook are **implied quantities**:

`implied quantity per kWh = published cost contribution per kWh ÷ published unit price`

For example, Argonne reports $25.76/kWh for LFP cathode active material and
$11.50/kg for its 2026 price. The implied intensity is therefore
25.76 ÷ 11.50 = **2.24 kg/kWh** for this specific design.

Carbon and binder remain an aggregate $/kWh line because Table 28 combines
multiple ingredients with different physical units and prices.

## External benchmark

[BloombergNEF's 2025 Battery Price Survey
release](https://about.bnef.com/insights/clean-transport/lithium-ion-battery-pack-prices-fall-to-108-per-kilowatt-hour-despite-rising-metal-prices-bloombergnef/)
reports average pack prices of $81/kWh for LFP and $70/kWh for stationary
storage. Those are observed global market averages, while the Argonne result
is a modeled U.S. automotive pack scenario, so the figures are context rather
than a like-for-like validation target.

## Key limitations

- The implied quantities are scenario-specific reconstruction values, not
  universal LFP material intensities.
- The sensitivity analysis holds design, yield, capacity, utilization, and all
  non-selected costs constant.
- The model does not reproduce BatPaC's electrochemical design calculations or
  process-level manufacturing model.
- A supplier quote also reflects qualification, volume commitments, capacity,
  geography, commercial terms, warranty, and negotiating leverage.
- The source scenario is automotive; a stationary-storage design could use
  different cell architecture, duty cycle, pack integration, and warranty
  assumptions.

## How to run

1. Clone the repository.
2. Install dependencies: `pip install matplotlib numpy`
3. Open `model.ipynb` in VS Code or Jupyter.
4. Run all cells from top to bottom.

## Stack

Python · NumPy · Matplotlib · Jupyter
