# LFP Battery Pack Should-Cost Model

This project breaks down the cost of a 75-kWh LFP battery pack and shows how
changes in major component prices affect the total cost.

It is based on a specific 2026 battery scenario published by Argonne National
Laboratory. It is a learning model, not a supplier quote.

## Result

- My reconstructed pack cost: **$102.08/kWh**
- Argonne's published result: **$102.20/kWh**
- Argonne's newer 2025 LFP estimate: **$101.74/kWh**

The small difference between my model and the source is caused by rounding in
Argonne's published tables.

## How it works

1. Take Argonne's unit price and cost contribution for each major component.
2. Calculate the implied material quantity:

   `quantity per kWh = cost per kWh ÷ unit price`

3. Add the remaining pack costs, including purchased items, manufacturing,
   overhead, profit, and warranty.
4. Test how the total changes when selected component prices move up or down
   by 30%.

For example, Argonne reports an LFP cathode cost of $25.76/kWh and a price of
$11.50/kg. That implies:

`$25.76/kWh ÷ $11.50/kg = 2.24 kg/kWh`

## Main findings

- Materials account for approximately **$55.58/kWh**, or 54% of pack cost.
- LFP cathode material is the largest cost driver at **$25.76/kWh**.
- A 30% change in the LFP cathode price changes total pack cost by approximately
  **$7.73/kWh**.

## Charts

![Cost Breakdown](cost_breakdown.png)
![Sensitivity Analysis](sensitivity.png)

## Sources

The model uses Argonne's
[*Cost of Automotive Batteries for Electric Vehicles - Update 2024*](https://publications.anl.gov/anlpubs/2024/01/187177.pdf):

- Tables 10-12: battery design and component prices
- Tables 27-28: pack and material cost breakdowns

Argonne's September 2025 update provides a newer comparison point of
**$101.74/kWh** for a similar 75-kWh LFP pack. I use it as a cross-check rather
than combining its inputs with the 2024 scenario because the cell designs are
different.

[BloombergNEF's 2025 Battery Price Survey](https://about.bnef.com/insights/clean-transport/lithium-ion-battery-pack-prices-fall-to-108-per-kilowatt-hour-despite-rising-metal-prices-bloombergnef/)
reports global average prices of $81/kWh for LFP packs and $70/kWh for
stationary-storage packs. These are market prices, while Argonne is a modeled
U.S. automotive pack cost, so they are useful context but not directly
comparable.

## Limitations

- The model represents one Argonne battery design, not every LFP battery.
- It holds the battery design and other costs constant during sensitivity tests.
- Actual supplier quotes also depend on volume, location, qualification,
  warranty, capacity, and commercial terms.

## Running the notebook

Install `matplotlib` and `numpy`, open `model.ipynb`, and run all cells from top
to bottom.
