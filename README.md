# Generative AI Environmental Impact Estimator

A scenario calculator for estimating the annual electricity, carbon and water associated with generative AI provided to staff and students under an institutional licence.

**[Open the calculator →](https://saundeg.github.io/genai-impact-estimator/)**

Constants version v4.0.

---

## Please read this first

This is **a scenario model, not a measurement.** It estimates what institutional AI use might plausibly consume, based on published research and a set of stated assumptions. It does not measure what your institution actually consumed, and it should never be presented as if it did.

It has not been endorsed by any institution. It is offered as a starting point for planning discussions in the period before suppliers provide actual usage data.

Nothing you type into the calculator is saved, transmitted or visible to anyone else. The whole calculation runs inside your own browser and everything you enter disappears when you close the tab.

---

## What it does

**If you already know how many queries an AI application handled** — many chatbots and assistants report this — enter that figure directly in the "Known applications" section at the top. Its energy is calculated from the measured count rather than from any assumption, and the same number of queries is then **subtracted from the modelled total**, because the weekly frequency below is defined as covering all your licensed tools. A measured query is already inside it. If every tool you use has a known figure, you can skip the headcount fields entirely.

For anything you don't have real data for, the tool works through a chain of multiplications:

1. **How many people use it.** Your headcount, multiplied by how many people use AI at all, multiplied by how much of that use runs through your institution's licence rather than personal free accounts.
2. **How often.** Mean interactions per active person per week, across the academic year.
3. **What kind of work.** Short questions, long reasoning tasks, agentic workflows, images and video consume very different amounts of energy. The tool weights them separately and blends the result.
4. **Convert to electricity.** Interactions × blended energy per interaction.
5. **Convert to carbon and water.** Using published conversion factors, including generation, transmission losses, the water evaporated cooling the data centre, and the water consumed generating the electricity upstream.
6. **Put it in proportion.** Per person, and as a share of institutional totals.

Every input is colour-tagged by how well evidenced it is:

| Tag | Meaning |
|---|---|
| **Measured** | Metered by the supplier in live production and published |
| **Published** | From peer-reviewed or formally published analysis |
| **Your data** | Only your institution can supply this |
| **Assumption** | Invented for planning. No published basis |

The answer is only as good as the weakest link in the chain, and several links are red.

---

## Read the scenarios, not the envelope

The tool's primary output is a comparison of three named scenarios — Cautious, Central and Intensive. Each is a coherent state of the world: a set of assumptions that could actually hold together. **These are the figures to quote.**

Underneath each headline there is also an *arithmetic envelope*. It is produced by setting every assumption to its bound at the same time. That is a useful sanity check on the model, but it is a corner of the parameter space with negligible plausibility, and it spans several hundredfold. It is **not** a confidence interval and **not** a probability statement. Do not put it in a return.

Earlier versions of this tool led with the envelope and asked readers not to quote the point estimate. That combination gave people nothing usable, and the predictable result was that the point estimate got quoted anyway without its caveats.

---

## Where the numbers come from

| What | Value | How solid is it? |
|---|---|---|
| Students using AI at all | 95% | **Strong, but read the caveat.** Published survey of 1,054 UK undergraduates, December 2025. It measures *ever-used*, so multiplying it by a weekly frequency treats occasional users as weekly ones and overstates the total |
| Staff using AI at all | 78% | **Weak.** No UK higher-education figure exists |
| Share of use on institutional licences | 45% / 60% | **No evidence.** Both invented. They exist only because real query counts aren't yet available — once you have one, enter it in Known applications instead |
| Mean interactions per person per week | 12 / 20 | **No evidence.** Invented. Enter the mean across all users, not the typical user: heavy users pull the mean well above the median |
| Energy, short text query | 0.31 Wh | **Strong.** Peer-reviewed, *Joule*, April 2026. Bounds are the paper's interquartile range |
| Energy, long reasoning query | 3.91 Wh | **Strong.** Same paper, ~5,000 output tokens |
| Model calls per agentic task | 4 / 8 / 16 | **Weak, and it dominates.** The multiplier is an assumption, and this category contributes roughly 70% of the central blended figure from 8% of queries |
| Energy, image generation | 0.3 / 2.9 / 11 Wh | **Moderate central, constructed high bound.** Measured by Luccioni et al., ACM FAccT 2024, across 88 models |
| Energy, video generation | 472 / 944 / 2,832 Wh per 5-sec clip | **Moderate central, constructed bounds.** Measured on CogVideoX, around 700× an image. A single unreplicated study, so the bounds are judgement, not published spread |
| Carbon per kWh, generation | 0.13096 kg | **Strong.** DESNZ 2026, location-based |
| Carbon per kWh, transmission losses | 0.01299 kg | **Strong.** DESNZ 2026, published 11 June 2026, down about 30% from 0.01853. Scope 3 category 3 |
| Carbon per kWh, market-based | 0.0958 kg | **Derived.** Google's Scope 2 electricity component only, 0.023 gCO₂e over 0.24 Wh |
| Data-centre cooling water | 0.36 L/kWh | **Moderate.** Published figures span 0.12 to about 1.1 |
| Upstream water from generation | 1.8 L/kWh | **Moderate.** Published values span 1.8 to 7.6 |

**Facility overhead (PUE) is deliberately not applied.** It is already inside both energy sources: Google decomposes its 0.24 Wh prompt as 0.14 Wh accelerators, 0.06 Wh host CPU and DRAM, 0.02 Wh idle capacity and 0.02 Wh data-centre overhead, and Oviedo et al. state their framework includes overhead. Applying a multiplier would count it twice.

---

## Three warnings

**The result will look trivially small, and that is a trap.** Even the intensive scenario rounds to nothing against a university's total footprint. That is a true statement about *inference within the chosen boundary*. It excludes training the models, manufacturing the chips, building the data centres, and the electricity users' own laptops draw. Those excluded items are where the large numbers live — Apple has reported that its supply chain accounts for 99% of its total corporate water footprint, cited in the literature as the clearest published illustration of how much larger supply-chain water use is than direct operational use. If this output is quoted as an all-in figure for AI's environmental impact, it will be seriously misleading.

**The sources have an interest in the answer.** Two of the three per-query energy figures come from Microsoft, and the third is Google reporting on itself. The Microsoft paper's central claim is that everyone else's published estimates are overstated by four to twenty times. That may well be correct — it is peer-reviewed and its method is transparent — but these outputs inherit that position, and any paper using them should say so.

**Two known biases remain, and they do not cancel.** All compute is costed at the UK grid factor, although inference for UK tenants is served substantially from Ireland, the Netherlands and the United States, where grid carbon is higher: this *understates*. And adoption is an ever-use measure multiplied by a weekly frequency: this *overstates*. Neither can be resolved without supplier data. Both are stated on screen alongside the output.

---

## Everyday comparisons

The calculator translates its results into human-scale comparisons — homes powered, miles driven, baths filled — because raw kilowatt-hours mean little to most readers.

These are **illustrative, never evidence.** The denominator you choose controls the impression entirely: the same quantity of electricity can be described as "what eight UK homes use in a year" or "what it takes to drive a petrol car 65,000 miles", and the choice between them is presentation rather than fact. The tool displays the basis for every comparison on screen, and any paper quoting one should quote its basis too. Never substitute a comparison for the actual figure.

| Comparison | Basis |
|---|---|
| UK home's annual electricity | 2,500 kWh — Ofgem typical domestic consumption value, reduced from 2,700 with effect from 1 July 2026 |
| Household water per person | 140 litres per day, about 51 m³ a year — England and Wales average |
| Driving an average petrol car | 0.17 kgCO₂e per km |
| Home electricity emissions | Fixed at the published DESNZ 2026 factor of 0.13096, deliberately held independent of the grid field in the tool so that editing an input cannot silently reframe the comparison |
| Olympic swimming pool | 2,500 m³ |
| Filled bath | 80 litres |

Note that most equivalence calculators online still use Ofgem's old 2,700 kWh household figure, which became out of date on 1 July 2026.

---

## Making a figure defensible later

A number published in a sustainability report gets challenged a year afterwards, by which time the defaults here will have moved. The tool therefore records enough to reconstruct any run:

- **Copy a link to this run** produces a URL containing every input. Anyone opening it sees exactly your figures.
- **Copy the assumptions log** produces a text record: constants version, run reference, boundary statement, every input with its evidence grade, the resulting figures, and the source vintage list.
- Every run carries a **constants version** and a **run hash**, so a figure can be tied to the state of the tool that produced it.

Quote the boundary statement alongside any figure. The log puts it first for that reason.

---

## Glossary

Grouped by topic rather than alphabetically, because the terms make more sense in clusters.

### Energy

**Watt-hour (Wh)** — a unit of energy. One watt-hour runs a one-watt device for an hour. A laptop charger draws around 45 watts, so a Wh is roughly a minute and a half of laptop charging.

**Kilowatt-hour (kWh)** — 1,000 watt-hours. The unit on an electricity bill. A UK household uses roughly 2,500 kWh a year (Ofgem, from 1 July 2026; the widely quoted 2,700 figure is now out of date).

**Megawatt-hour (MWh)** — 1,000 kWh. The tool switches to this unit automatically once numbers get large.

**Inference** — an already-built AI model answering a question. This is what the tool measures. Distinguished from **training**, the much larger one-off effort of building the model, which is excluded.

**Token** — the unit AI models read and write in, roughly three-quarters of a word. Energy scales mainly with how many tokens the model *writes*, which is why long answers cost far more than short ones.

**Long reasoning query** — where the model works through a problem at length before answering, producing around 5,000 output tokens. Costs roughly thirteen times a standard query.

**Agentic workflow** — where the AI performs a multi-step task on its own: searching, reading, writing code, checking its work. One action to the user; many separate model calls to the data centre. The tool models this as a multiple of a long reasoning query, which is a simplification: it does not represent the large input contexts real agentic calls carry, nor retrieval, safety passes, retries or reasoning tokens you never see.

**PUE (Power Usage Effectiveness)** — total electricity a data centre draws for every unit reaching the actual computers. A PUE of 1.1 means 10% overhead for cooling and power conversion. Lower is better. Google reports about 1.09 across its fleet. This tool does not apply a PUE multiplier, because overhead is already inside both of its energy sources.

### Carbon

**CO₂e (carbon dioxide equivalent)** — a common unit for all greenhouse gases, converting each into the amount of CO₂ causing equivalent warming.

**Emission factor**, or **conversion factor** — the number you multiply an activity by to get emissions. For electricity, expressed in kgCO₂e per kWh.

**DESNZ** — the UK Department for Energy Security and Net Zero, which publishes the official annual conversion factors for UK carbon reporting. Still widely called "the Defra factors" after the department that used to publish them. The 2026 electricity generation factor is 0.13096 kgCO₂e/kWh, with transmission and distribution losses a further 0.01299.

**Location-based emissions** — calculated using the average carbon content of the grid where the power was consumed. Answers: what did the grid have to burn?

**Market-based emissions** — calculated after crediting the renewable energy certificates and power purchases the supplier has made. Answers: what did this organisation pay for?

> **A correction worth reading.** Earlier versions of this guide said the two bases can differ by an order of magnitude for the same electricity. That was wrong, and the tool displayed a fifteen-fold gap because of an arithmetic error rather than an accounting one. On Google's own paired disclosure, the market-based factor works out at about 0.0958 kgCO₂e/kWh against DESNZ's location-based 0.13096 — roughly 1.3× apart, not tenfold. Large divergences do occur at the level of a whole supplier's corporate reporting, but not per unit of electricity on these figures.

**Scope 1, 2 and 3** — the standard split of an organisation's emissions. Scope 1 is what you burn directly, Scope 2 is electricity you buy, Scope 3 is everything else in your value chain. Third-party AI services sit in your Scope 3, and so do transmission and distribution losses.

**SECR** — Streamlined Energy and Carbon Reporting, the UK regime requiring larger organisations to report energy and emissions in their annual accounts. Location-based is the reported basis for electricity, with market-based permitted as additional disclosure.

### Water

**Withdrawal versus consumption** — withdrawal is water taken from a source; consumption is water that does not come back, usually because it evaporated. Consumption causes local scarcity and is what this tool estimates.

**Direct water** — evaporated on-site cooling the data centre.

**Indirect water** — consumed upstream at the power station generating the electricity. Frequently 80% or more of the true total.

**WUE (Water Usage Effectiveness)** — litres of water consumed per kWh delivered to computing equipment. Standardised as ISO/IEC 30134-9. A WUE of zero means no water is used for cooling at all, achievable with closed-loop or air-cooled designs.

### Statistics

**Median** — the middle value when observations are lined up in order. Preferred over the average because a few enormous queries would drag an average upward.

**Interquartile range (IQR)** — the middle half of observations, 25th to 75th percentile. "Median 0.31 Wh, IQR 0.16–0.60" means half of all queries fell in that band — not that it's an absolute minimum and maximum. The tool currently bounds its two best-evidenced energy parameters at the IQR, which by construction excludes half the published distribution. Widening these to the source's P5 and P95 is an open item.

**Order of magnitude** — a factor of ten. Saying an estimate is accurate to an order of magnitude means the true value is probably between a tenth and ten times the figure given. That is the honest accuracy claim here, which is why headline figures render at two significant figures and percentages at one.

**Boundary** — what a calculation counts and what it leaves out. Two studies of "AI's environmental impact" can differ a hundredfold purely because they drew different boundaries. Comparing figures without checking their boundaries is the most common error in this field.

---

## What would improve this most

1. **Ask your suppliers for usage counts.** Microsoft, Google and OpenAI enterprise agreements can report prompt or token volumes at tenant level. Actual interaction counts would remove the two weakest assumptions in one step. Where a figure is already available — an internal chatbot or assistant, for example — enter it in Known applications rather than folding it into the scenario percentages.
2. **Ask which regions serve your tenant, and for their WUE and PUE.** The tool currently costs all compute at the UK grid factor, which is very likely wrong. EU rules now require data centres above 500 kW to report water use annually.
3. **Decide the reporting basis before the number is needed.** Location-based or market-based; direct water only or direct plus upstream. Settling this in advance stops the tool being tuned after the fact.

A note on the second point, from experience: if your supplier's sustainability dashboard offers no location-based figure, no service-level breakdown, and a footnote disclaiming use for reporting purposes, that is itself a finding worth documenting. A disclosure gap is actionable through procurement in a way that a modelled number is not.

---

## Version history

- **v4.0** — Corrected the transmission factor to the DESNZ 2026 vintage; split the market-based factor to its Scope 2 electricity component; applied transmission losses to both accounting bases; deducted measured queries from the modelled total rather than adding them on top; added bounds to the agentic multiplier; made the three scenarios the primary output and demoted the envelope.
- **v3.0** — Fixed market-based carbon to derive from kWh rather than a flat per-prompt rate; added uncertainty bounds to licence share and interaction frequency; added the audit trail, shareable runs and permanent exclusions panel.
- **v2.0** — Known applications section; evidence grading; everyday comparisons.

Both change notes are held in this repository.

---

## Sources

- Oviedo, F. et al., "Energy use of AI inference, efficiency pathways, and test-time scaling," *Joule*, 22 April 2026. [doi:10.1016/j.joule.2026.102430](https://doi.org/10.1016/j.joule.2026.102430) · [preprint](https://arxiv.org/abs/2509.20241)
- Google, "Measuring the environmental impact of AI inference," Google Cloud blog, 21 August 2025, and accompanying technical paper
- Microsoft, "Scaling AI with 8 to 20x energy efficiency," Microsoft Cloud blog, 15 June 2026
- Stephenson, R. and Armstrong, C., *Student Generative AI Survey 2026*, HEPI Report 199 with Kortext
- Department for Energy Security and Net Zero, *Greenhouse gas reporting: conversion factors 2026*, published 11 June 2026
- Li, P., Yang, J., Islam, M.A. and Ren, S., "Making AI Less Thirsty," *Communications of the ACM*
- Lawrence Berkeley National Laboratory, *2024 United States Data Center Energy Usage Report*
- Luccioni, S., Jernite, Y. and Strubell, E., "Power Hungry Processing: Watts Driving the Cost of AI Deployment?", *ACM FAccT*, 2024 — measured image generation; the video figure comes from the same author's later CogVideoX measurements
- International Energy Agency, *Energy and AI*, 2025
- Ofgem, *Review of typical domestic consumption values*, decision implemented 1 July 2026 — for the household electricity comparison
- Ofwat and Water UK, for average household water consumption per person

---

## Reuse

Offered for reuse and adaptation by other institutions. If you improve the assumptions — particularly if you obtain real supplier usage data — please consider sharing what you find, since nobody in the sector currently has good numbers on this.
