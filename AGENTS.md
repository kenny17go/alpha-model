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


## 9. Alpha Model must be AI's research memory, not a replacement for AI

The reason Alpha Model exists is to prevent AI from restarting company and industry research from zero on every question.

Core division of labor:

**Program/database remembers; AI interprets.**

The system should continuously collect, normalize, preserve, and update reusable evidence. AI should receive a compact, structured research context and spend its effort on interpretation, exceptions, expectation gaps, and model improvement.

If AI still needs to re-research most of a company from scratch every time, the module has failed its purpose.

### AI Context Pack

Each company and industry comparison should be able to generate a compact AI Context Pack containing only the information needed for analysis:
- industry module and current version;
- standardized shared KPIs and recent changes;
- company-specific KPIs that have already been validated;
- Our Base;
- Market Expectation;
- Expectation Gap;
- current price and external analyst Low / Avg / High;
- relevant Research Memory;
- unresolved questions;
- primary-source references.

The prompt should explicitly tell AI not to re-search information already present unless the context is insufficient or stale.

Provide one-click prompt actions such as:
- analyze the current expectation gap;
- explain today's material changes;
- compare companies in the same industry;
- check whether the module is missing a material KPI;
- reassess Our Base;
- deep-dive only where the existing context is insufficient.

## 10. AI findings must accumulate through a controlled Research Memory

Do not save long AI answers as the model's knowledge base.

Convert useful new findings into small structured records such as:
- New KPI;
- New Evidence;
- Expectation Change;
- Model Suggestion.

New AI findings must enter an **AI Research Inbox** first. They do not become formal model rules automatically.

Preferred lifecycle:

**AI Finding → Research Inbox → human/verification review → Research Memory → Company Rule → Industry Rule**

Only promote a finding when evidence supports it. Preserve source, date, affected company/module, rationale, confidence, and verification status.

This prevents one incorrect AI answer from contaminating the formal model while allowing useful research to compound over time.

## 11. The model must learn from forecast errors

For every forecast period, preserve:
- Our Base at the time;
- Market Expectation at the time;
- Actual result;
- forecast error;
- market expectation error where available;
- the KPI/assumption that caused the largest error;
- what was learned.

After Actual is available, perform a lightweight post-mortem rather than simply overwriting the old forecast.

The objective is to learn which KPIs actually improve expectation-gap judgment and which add noise.

## 12. Model changes require explicit versioning and validation

AI may propose model changes, but it must not silently modify the formal industry model.

Preferred lifecycle:

**Forecast vs Actual → error diagnosis → AI/model suggestion → Model Change Inbox → review → new Model Version → subsequent validation**

Track whether a new version improves:
- forecast error;
- ability to explain Expectation Gap;
- cross-company comparability;
- research time / AI re-search required;
- KPI count and complexity.

A better model does **not** necessarily contain more KPIs. Prefer a smaller set of KPIs when it provides equal or better explanatory and forecasting value.

Example of healthy evolution:

**V1: 12 KPIs → V2: 9 KPIs → V3: 6 KPIs, with lower error and clearer expectation-gap explanation**

## 13. Module Validation Gate — validate before scaling

Do not add more companies, industries, KPIs, or data sources merely to increase coverage.

Before scaling an industry module, test whether the existing module can provide roughly **60–70% of the analytical foundation without AI starting research from zero**.

A module should answer three questions:
1. Can the shared KPIs compare companies meaningfully despite differences in maturity and business mix?
2. Can the stored evidence explain why Our Base differs from Market Expectation?
3. Can a new peer be mapped into the module without redesigning the model from scratch?

If the answer is no, fix or simplify the module before adding more coverage.

For automotive semiconductors, use **INDI / NXPI / ON** as the current validation set. Do not add a fourth peer until the module passes this validation gate.

Do not force every company to disclose identical leading indicators. A mature company may prove conversion through production/revenue results while an earlier-stage company may require Design Win / SOP evidence.

A practical shared structure may therefore be:

**Growth → Profitability → Cash**
+
**Conversion layer appropriate to company maturity**
+
**Company-specific KPI only when it materially explains Expectation Gap**

## 14. Efficiency is a first-class model metric

Alpha Model should become cheaper and faster to use as knowledge accumulates.

A successful module should reduce:
- repeated web research;
- repeated AI token/context usage;
- duplicated company-specific analysis;
- number of low-value KPIs;
- time required to identify the key expectation-gap driver.

When choosing between “collect more” and “make existing knowledge more reusable,” prefer reuse unless new evidence can materially change the analytical conclusion.

## Updated development sequence

Until the automotive-semiconductor validation is complete, prioritize:

**Module Validation → AI Context Pack → one-click AI prompts → AI Research Inbox → Research Memory → Forecast vs Actual → Model Change Inbox → Model Version / backtest**

Do not expand coverage before this loop works end-to-end.

The long-term objective is a compounding research system:

**automatic data collection → reusable industry module → compact AI context → AI interpretation → verified new knowledge → model memory → forecast validation → controlled model improvement**

The system should become more accurate and more efficient through use, not merely larger.
