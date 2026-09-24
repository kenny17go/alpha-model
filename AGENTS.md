# Alpha Model — Development Guardrails

This file is the persistent development rule for Alpha Model. Read it before making product, data-model, analysis, UI, or automation changes.

## North Star

Alpha Model is **not** primarily a single-stock research terminal and is **not** a tool whose goal is to calculate an absolute target price.

Its purpose is to discover **expectation gaps** from public market information:

**Industry module → standardized KPI evidence → AI-assisted company-specific KPI review → Our Base → Market Expectation → Expectation Gap → current-price context / external analyst range → candidates for further research**

The goal is to identify cases where market expectations may be too optimistic or too pessimistic relative to observable fundamental evidence.

## 1. Industry module first

Build reusable models by **industry**, not one bespoke model per company.

A mature industry module should explain roughly **60–70%** of the recurring analytical work using standardized, collectible KPIs and rules.

Examples:
- Automotive semiconductors: Design Wins → SOP / Production → Revenue → Profitability → Cash
- Financial holding companies: Bank NII / Credit Cost → Life CSM / Capital → Subsidiary Earnings → Group Earnings / ROE / Capital

When a company is added, first map it to an existing industry module. Only create company-specific logic for material differences that the shared module cannot explain.

## 2. AI is the supplement, not the core model

AI should help identify:
- company-specific KPIs not covered by the industry module;
- unusual events or disclosures;
- which KPI changes matter to the thesis;
- why Our Base may differ from Market Expectation.

AI should **not** replace the standardized industry framework with an opaque score or unconstrained narrative.

## 3. Stop research when the expectation gap can be judged

Do not keep collecting data simply because more data exists.

Deep research should stop once there is enough reliable evidence to answer:
1. What does the market currently expect?
2. What is Our Base based on industry/company KPIs?
3. Where do the two differ?
4. Which KPI or assumption explains the difference?

More data is justified only if it can materially change one of those answers.

## 4. The key output is Expectation Gap

The primary analytical comparison is:

**Our Base vs Market Expectation**

For comparable metrics:

**Expectation Gap = Our Base / Market Expectation − 1**

A high growth rate alone is not Alpha. If the market already expects more growth, there may be no positive expectation gap. Likewise, a modest-growth company may be interesting if observable KPIs imply better fundamentals than the market currently expects.

The system must support both directions:
- market expectations may be too pessimistic;
- market expectations may be too optimistic.

## 5. Price is context, not an absolute truth

Do **not** require Alpha Model to calculate a single “correct” fair value or target price.

Use external analyst price targets (for example Low / Average / High) as a **benchmark**, together with current price, to show where the stock currently sits within the external expectation range.

External analyst targets do not replace Alpha Model's fundamental judgment and are not Alpha Model's own target price.

Useful display:
**Current Price | Analyst Low / Avg / High | Our Base | Market Expectation | Expectation Gap | key KPI causing the gap**

## 6. Separate collection from presentation

Backend/research storage can remain detailed:
- KPI history
- SEC / MOPS / official documents
- source URLs
- production milestones
- automation metadata
- historical observations

Frontend should remain concise.

Default view should answer:
- What changed?
- What does the market expect?
- What do we expect?
- What is the gap?
- What KPI explains the gap?
- Where is current price relative to the analyst range?

Detailed evidence stays collapsed or in the research layer.

## 7. Cross-company comparison is the end goal

The final purpose of an industry module is to put **all relevant companies in the same industry through the same comparable framework**.

The system should make it easy to compare companies using consistent industry KPIs and expectation gaps, so the user can identify which names deserve further research and which may already reflect optimistic expectations.

Do not turn this into an automatic buy/sell ranking. Surface evidence and expectation differences; the investment decision remains with the user.

## 8. Development priority test

Before adding a feature, source, KPI, model, or database table, ask:

**Does this materially improve the industry's reusable 60–70% framework, Our Base, Market Expectation, Expectation Gap, or cross-company comparison?**

If not, defer it.

In particular, avoid:
- endless single-company deep dives;
- adding data sources without a defined analytical use;
- forcing DCF / P-E / target-price models on every company;
- exposing every collected KPI on the main UI;
- creating bespoke logic that should belong in an industry template;
- mistaking “more data” for “better Alpha detection.”

## Current implementation direction

INDI is the first validation case for the automotive-semiconductor module. Do not keep deepening INDI by default. Use what was learned from INDI to make the automotive-semiconductor module reusable and test it on additional companies.

Other candidates should follow the same architecture: industry module first, company-specific exceptions second, then Our Base vs Market Expectation and price-context comparison.
