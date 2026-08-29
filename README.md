# Generative AI Environmental Impact Estimator

A scenario calculator for estimating the annual electricity, carbon and water associated with generative AI provided to staff and students under an institutional licence.

**[Open the calculator →](https://saundeg.github.io/genai-impact-estimator/)**

---

## Please read this first

This is **a scenario model, not a measurement.** It estimates what institutional AI use might plausibly consume, based on published research and a set of stated assumptions. It does not measure what your institution actually consumed, and it should never be presented as if it did.

It has not been endorsed by any institution. It is offered as a starting point for planning discussions in the period before suppliers provide actual usage data.

Nothing you type into the calculator is saved, transmitted or visible to anyone else. The whole calculation runs inside your own browser and everything you enter disappears when you close the tab.

---

## What it does

It works through a chain of multiplications:

1. **How many people use it.** Your headcount, multiplied by how many people use AI at all, multiplied by how much of that use runs through your institution's licence rather than personal free accounts.
2. **How often.** Interactions per active person per week, across the academic year.
3. **What kind of work.** Short questions, long reasoning tasks, agentic workflows and image generation consume very different amounts of energy. The tool weights them separately and blends the result.
4. **Convert to electricity.** Interactions × blended energy per interaction.
5. **Convert to carbon and water.** Using published conversion factors, including both the water evaporated cooling the data centre and the water consumed generating the electricity upstream.
6. **Put it in proportion.** Express the result as a share of institutional totals.

Every input is colour-tagged by how well evidenced it is:

| Tag | Meaning |
|---|---|
| **Measured** | Metered by the supplier in live production and published |
| **Published** | From peer-reviewed or formally published analysis |
| **Your data** | Only your institution can supply this |
| **Assumption** | Invented for planning. No published basis |

The answer is only as good as the weakest link in the chain, and several links are red.

---

## Where the numbers come from

| What | Value | How solid is it? |
|---|---|---|
| Students using AI at all | 95% | **Strong.** Published survey of 1,054 UK undergraduates, December 2025 |
| Staff using AI at all | 78% | **Weak.** No UK higher-education figure exists |
| Share of use on institutional licences | 45% / 60% | **No evidence.** Invented — replace this first |
| Interactions per person per week | 12 / 20 | **No evidence.** Invented |
| Energy, short text query | 0.31 Wh | **Strong.** Peer-reviewed, *Joule*, April 2026 |
| Energy, long reasoning query | 3.91 Wh | **Strong.** Same paper, ~5,000 output tokens |
| Energy, agentic task | 8 × long query | **Weak.** The multiplier is an assumption |
| Energy, image or video | 2.5 Wh | **None.** Placeholder — no production benchmark exists |
| Carbon per kWh | 0.13096 kg | **Strong.** UK government official factor, 2026 |
| Data-centre cooling water | 0.36 L/kWh | **Moderate.** Published figures span 0.12 to about 1.1 |
| Upstream water from generation | 1.8 L/kWh | **Moderate.** Published values span 1.8 to 7.6 |

---

## Two warnings

**The result will look trivially small, and that is a trap.** Even the intensive scenario rounds to nothing against a university's total footprint. That is a true statement about *inference within the chosen boundary*. It excludes training the models, manufacturing the chips, building the data centres, and the electricity users' own laptops draw. Those excluded items are where the large numbers live — one major operator reports that supply-chain water alone exceeds 99% of its corporate water footprint. If this output is quoted as an all-in figure for AI's environmental impact, it will be seriously misleading.

**The sources have an interest in the answer.** Two of the three per-query energy figures come from Microsoft, and the third is Google reporting on itself. The Microsoft paper's central claim is that everyone else's published estimates are overstated by four to twenty times. That may well be correct — it is peer-reviewed and its method is transparent — but these outputs inherit that position, and any paper using them should say so.

---

## Glossary

Grouped by topic rather than alphabetically, because the terms make more sense in clusters.

### Energy

**Watt-hour (Wh)** — a unit of energy. One watt-hour runs a one-watt device for an hour. A laptop charger draws around 45 watts, so a Wh is roughly a minute and a half of laptop charging.

**Kilowatt-hour (kWh)** — 1,000 watt-hours. The unit on an electricity bill. A UK household uses roughly 2,700 kWh a year.

**Megawatt-hour (MWh)** — 1,000 kWh. The tool switches to this unit automatically once numbers get large.

**Inference** — an already-built AI model answering a question. This is what the tool measures. Distinguished from **training**, the much larger one-off effort of building the model, which is excluded.

**Token** — the unit AI models read and write in, roughly three-quarters of a word. Energy scales mainly with how many tokens the model *writes*, which is why long answers cost far more than short ones.

**Long reasoning query** — where the model works through a problem at length before answering, producing around 5,000 output tokens. Costs roughly thirteen times a standard query.

**Agentic workflow** — where the AI performs a multi-step task on its own: searching, reading, writing code, checking its work. One action to the user; many separate model calls to the data centre.

**PUE (Power Usage Effectiveness)** — total electricity a data centre draws for every unit reaching the actual computers. A PUE of 1.1 means 10% overhead for cooling and power conversion. Lower is better. Google reports about 1.09 across its fleet.

### Carbon

**CO₂e (carbon dioxide equivalent)** — a common unit for all greenhouse gases, converting each into the amount of CO₂ causing equivalent warming.

**Emission factor**, or **conversion factor** — the number you multiply an activity by to get emissions. For electricity, expressed in kgCO₂e per kWh.

**DESNZ** — the UK Department for Energy Security and Net Zero, which publishes the official annual conversion factors for UK carbon reporting. Still widely called "the Defra factors" after the department that used to publish them. The 2026 electricity factor is 0.13096 kgCO₂e/kWh.

**Location-based emissions** — calculated using the average carbon content of the grid where the power was consumed. Answers: what did the grid have to burn?

**Market-based emissions** — calculated after crediting the renewable energy certificates the supplier has bought. Answers: what did this organisation pay for? The two can differ by an order of magnitude for the same electricity, which is why the tool shows both. Google's published 0.03 gCO₂e per prompt is market-based.

**Scope 1, 2 and 3** — the standard split of an organisation's emissions. Scope 1 is what you burn directly, Scope 2 is electricity you buy, Scope 3 is everything else in your value chain. Third-party AI services sit in Scope 3.

**SECR** — Streamlined Energy and Carbon Reporting, the UK regime requiring larger organisations to report energy and emissions in their annual accounts.

### Water

**Withdrawal versus consumption** — withdrawal is water taken from a source; consumption is water that does not come back, usually because it evaporated. Consumption causes local scarcity and is what this tool estimates.

**Direct water** — evaporated on-site cooling the data centre.

**Indirect water** — consumed upstream at the power station generating the electricity. Frequently 80% or more of the true total.

**WUE (Water Usage Effectiveness)** — litres of water consumed per kWh delivered to computing equipment. Standardised as ISO/IEC 30134-9. A WUE of zero means no water is used for cooling at all, achievable with closed-loop or air-cooled designs.

### Statistics

**Median** — the middle value when observations are lined up in order. Preferred over the average because a few enormous queries would drag an average upward.

**Interquartile range (IQR)** — the middle half of observations, 25th to 75th percentile. "Median 0.31 Wh, IQR 0.16–0.60" means half of all queries fell in that band — not that it's an absolute minimum and maximum.

**Order of magnitude** — a factor of ten. Saying an estimate is accurate to an order of magnitude means the true value is probably between a tenth and ten times the figure given. That is the honest accuracy claim here.

**Boundary** — what a calculation counts and what it leaves out. Two studies of "AI's environmental impact" can differ a hundredfold purely because they drew different boundaries. Comparing figures without checking their boundaries is the most common error in this field.

---

## What would improve this most

1. **Ask your suppliers for usage counts.** Microsoft, Google and OpenAI enterprise agreements can report prompt or token volumes at tenant level. Actual interaction counts would remove the two weakest assumptions in one step.
2. **Ask for their WUE and PUE at the regions serving you.** Both are increasingly disclosed, and EU rules now require data centres above 500 kW to report water use annually.
3. **Decide the reporting basis before the number is needed.** Location-based or market-based; direct water only or direct plus upstream. Settling this in advance stops the tool being tuned after the fact.

---

## Sources

- Oviedo, F. et al., "Energy use of AI inference, efficiency pathways, and test-time scaling," *Joule*, 22 April 2026. [doi:10.1016/j.joule.2026.102430](https://doi.org/10.1016/j.joule.2026.102430) · [preprint](https://arxiv.org/abs/2509.20241)
- Google, "Measuring the environmental impact of AI inference," Google Cloud blog, 21 August 2025, and accompanying technical paper
- Microsoft, "Scaling AI with 8 to 20x energy efficiency," Microsoft Cloud blog, 15 June 2026
- Stephenson, R. and Armstrong, C., *Student Generative AI Survey 2026*, HEPI Report 199 with Kortext
- Department for Energy Security and Net Zero, *Greenhouse gas reporting: conversion factors 2026*
- Li, P., Yang, J., Islam, M.A. and Ren, S., "Making AI Less Thirsty," *Communications of the ACM*
- Lawrence Berkeley National Laboratory, *2024 United States Data Center Energy Usage Report*
- International Energy Agency, *Energy and AI*, 2025

---

## Reuse

Offered for reuse and adaptation by other institutions. If you improve the assumptions — particularly if you obtain real supplier usage data — please consider sharing what you find, since nobody in the sector currently has good numbers on this.
