# Proposal: Building an Automated Pipeline for 1000 ICP-Qualified Companies in 30 Days
**Prepared by:** Rehan M Jatti
**Target Metric:** 1000 Verified "Federer" Companies (Indian Specialty Manufacturers, Rs.50Cr–Rs.500Cr)

---

## 🗺️ Architectural Workflow Overview

To deliver a high-integrity, quality-first database of 1000 qualified companies within 30 calendar days, the workflow operates as a strictly structured data funnel. We anticipate a ~30% macro yield based on historical baseline trends, meaning our raw ingestion universe must comprise roughly 3,500–4,000 unique companies.

Universe Sourcing Ingestion (3,500 - 4,000 Unstructured Targets)
↓ Programmatic String Match Pre-Filters (Auto-Reject Drop)
Screened Company Pool (2,000 - 2,500 Active Domains)
↓ Automated Scraper Infrastructure (Playwright + 8k Max Token Cap)
First-Pass LLM Grading Pipeline (Claude Haiku Programmatic JSON Export)
↓ High-Confidence Passes (60-100) vs. Borderline Routing (40-48 Total Score)
Deep LLM Evaluation / Re-Scoring (Claude Sonnet Analytical Evaluation)
↓ Auto-QA Programmatic Filtering (Flagging Stale Logs or Low-Moat Flags)
Human QA Oversight Verification (Targeted manual spot-checks on edge cases)
↓ Final Production Export
1000 Fully Verified "Federer" List (With High-Impact Outbound Personalization Hooks)


---

## 📆 Chronological Weekly Execution Timeline

### 🛠️ Week 1: Universe Ingestion & Web Discovery
*   **Focus:** Bulk data pulling and deduplication. No multi-tier scoring happens here—only gathering raw business names, cities, and primary domains.
*   **Tactics:** Download public master data registers (DSIR unit sheets, BSE SME ticker maps, USFDA certified facility lists). Run automation sequences to pull directories from 6 major targeted B2B expos.
*   **Deduplication Layer:** Deploy fuzzy text logic (Levenshtein distance scoring) to catch and merge corporate duplicates (e.g., merging "XYZ Chemicals Pvt. Ltd." and "XYZ Chemicals Private Limited"). Run automated Google searches (`{Company Name} + {City} + site:.in`) for any entries missing a baseline website domain URL.
*   **Target Output:** A clean, deduplicated universe sheet containing 3,500–4,000 raw entities.

### 🤖 Week 2: Scraper Deployment & Core Ingestion
*   **Focus:** Full-scale automated web scraping and token consolidation.
*   **Scraper Architecture:** A Python script utilizing Playwright to handle modern, JavaScript-heavy sites. For every discovered domain, the scraper targets 5-8 vital subpages: `/homepage`, `/about-us`, `/products`, `/management`, `/careers`, and `/news`.
*   **Data Safeguards:** Implement polite 10-second processing timeouts and respect `robots.txt` instructions to prevent IP blocking. Text content is stripped of HTML noise, capped at 8,000 tokens per domain, and stored systematically.

### 🧠 Week 3: Programmatic Two-Tier LLM Evaluation
*   **Focus:** Direct algorithmic grading against the Federer framework.
*   **Tier 1 (Haiku Ingestion):** The 8,000-token payload is dispatched to Claude Haiku with a strict engineering prompt. Haiku checks the eligibility gates ($E1$/$E2$) and returns a clean JSON structure containing individual numerical weights for criteria $C3$ through $C8$, complete with short text evidence strings and internal confidence markers.
*   **Tier 2 (Sonnet Deep Dive):** To control API expenses while ensuring deep accuracy, any company returning an open borderline score (40–48 range) or tripping a "low confidence" marker is routed to Claude Sonnet for analytical re-evaluation.
*   **Target Output:** An initial database output containing ~1,200–1,400 raw system passes.

### 🔍 Week 4: Multi-Layer Quality Assurance & Delivery
*   **Focus:** Programmatic cleaning and manual evaluation of edge cases.
*   **Programmatic Flags:** Build script rules to catch and flag common AI hall-of-fame errors:
    *   Flag any profile citing generic "ISO 9001" as proof of high technical differentiation ($C3$).
    *   Flag profiles utilizing outdated media listings (older than 2024) to argue for active growth status ($C6$).
*   **Human QA Review:** Dedicate structured manual review blocks to look into the 300–400 system-flagged edge profiles. Spend 3-4 minutes per company to manually review the core website, adjust faulty point assignments, and drop poor-fitting targets.
*   **Final Output Polish:** Filter out the highest-scoring entries, extract personalized first-line email hooks for the top 200 high-priority records, and format the output into a clean, ready-to-use CSV sheet.

---

## 📊 Expected Data Funnel & Yield Dynamics

Based on strict alignment with the baseline criteria outlined in the assignment documents, the pipeline accounts for systematic attrition at every stage of execution:

| Funnel Phase | Sizing Metrics | Expected Attrition Vector | Remaining Pool |
| :--- | :--- | :--- | :--- |
| **Raw Universe Ingestion** | 4,000 Companies | Baseline Ingestion Point | 4,000 |
| **String-Match Pre-Filtering** | -800 Companies | Eliminates clear trading firms, distributors, and massive conglomerates via master string logs | 3,200 |
| **Eligibility Gate Processing** | -1,100 Companies | Rejects entities failing structural $E1$ or $E2$ benchmarks (service-only operations or unlisted generic pharma) | 2,100 |
| **LLM Evaluation & Re-Scoring** | -800 Companies | Filters out businesses sitting below the 60-point target threshold (stagnant entities or low-system setups) | 1,300 |
| **Automated QA & Manual Oversight** | -300 Companies | Drops false positives, resolves edge profiles, and filters out missing datasets | 1,000 |
| **Final Production Output** | **1,000 Companies** | **Fully verified, target-ready entities matching the definitive A/B Federer bands** | **1,000** |

---

## 🛠️ Infrastructure, Tooling, & Financial Cost Forecast

By using a two-tier LLM evaluation framework, cloud compute requirements and API overhead expenses are kept lean and cost-effective:

*   **Claude Haiku API:** Powers 100% of the initial data processing passes (~3,500 evaluations × Rs. 0.40 average token processing cost) = **~Rs. 1,400**
*   **Claude Sonnet API:** Reserves deep contextual processing for borderline profiles and complex edge instances (~700 evaluations × Rs. 3.50 token processing cost) = **~Rs. 2,450**
*   **Web Scraping Logic:** Python + Playwright Framework (Open-Source / Free local compute execution)
*   **Development / Script Support:** GitHub Copilot (Enterprise workspace access provided by organization)
*   **Corporate Record Lookup:** Antigravity / Ministry of Corporate Affairs data portal (Workspace access provided by organization)
*   **Total Projected Infrastructure Budget:** **~Rs. 3,850**