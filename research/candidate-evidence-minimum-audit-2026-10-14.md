# Candidate Evidence Minimum Audit — 2026-10-14

Scope: original Candidate companies GRAB, SE, RBLX only. This is a data-quality and research-readiness audit, **not** a model revision or an investment recommendation. NXPI/ON are industry references, not Candidates.

## Existing observations (database snapshot)

- **GRAB**: four Q2 2026 observations (GMV, profitability, financial_services, FCF), sourced to [SEC earnings release](https://www.sec.gov/Archives/edgar/data/1855612/000185561226000125/a52026q2-earningspressrele.htm). No earlier quarter observations in the inspected set. **Gap:** aligned prior quarters and precise definitions, then determine whether GMV growth translates into profitability/FCF. Do not infer a trend from one quarter.
- **SE**: Q1 and Q2 2026 observations for Shopee, Monee, Garena; group_cash Q2 YTD. Q2 source: [SEC earnings exhibit](https://www.sec.gov/Archives/edgar/data/1703399/000119312526344596/d120948dex991.htm). Q1 source: [Sea investor results](https://cdn.sea.com/investor/1Q2026/HEEdeRDe0NyiZ1PrWIvH/2026.05.12%20Sea%20First%20Quarter%202026%20Results.pdf). **Data quality blocker:** Monee observations 1200 (Q1) vs 11100 (Q2) may represent different concepts/units. Recheck source line and metric definition before calculating growth. YTD cash must not be compared to a single quarter.
- **RBLX**: Q2 2025 and Q2 2026 observations for bookings, engagement, monetization, FCF. Q2 2026 source: [SEC earnings exhibit](https://www.sec.gov/Archives/edgar/data/1315098/000162828026051059/ex991-robloxq22026earnin.htm); Q2 2025 source: [Roblox IR](https://ir.roblox.com/news/news-details/2025/Roblox-Reports-Second-Quarter-2025-Financial-Results/default.aspx). **Data quality blocker:** monetization 12.86 (Q2 2025) vs 0.139 (Q2 2026) appears non-comparable; verify metric definition and units. Engagement 111.8 vs 123 requires matching units. No automated YoY calculations until reconciled.

## Minimum evidence standard

1. **One authoritative primary source per metric**, with source URL, metric definition, unit, period, fiscal basis and collection timestamp.
2. **Comparable history**: prefer four recent quarters, or a verified YoY comparable pair when sufficient for the specific thesis question; mark missing history instead of inventing values.
3. **Thesis linkage**: one line per company: evidence supports, contradicts or is inconclusive for the existing Operating Driver. No auto-edit to Our Base/Thesis.
4. **Stop condition**: once core metrics are definition-checked and each thesis has a clear next verification, stop Candidate expansion. Resume Watch List, Expectation Gap, Thesis Change Detection.

## Next limited actions

- GRAB: backfill only comparable GMV, adjusted operating profitability, FCF.
- SE: resolve Monee metric mismatch first; then Shopee unit economics / profitability and credit quality evidence if published.
- RBLX: resolve monetization unit mismatch first; compare bookings and engagement on consistent basis.
- Leave `evidence_gap` until verified. Do not call Candidate module completion an investment signal.

## Return to core

Next product work should be **Watch List daily meaningful changes → same-period Our Base vs Market Expectation → evidence-driven Thesis Change Detection**. No new industries, no Candidate ranking, no new score.
