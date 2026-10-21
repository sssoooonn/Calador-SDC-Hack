# Aiversecity – AI Career & Skills Navigator

A proof-of-concept web app for the **Aiversecity Future-Ready Workforce Domain**. It takes a user from "who I am today" to "where I can be in the AI era": profile → future skills radar → ranked future roles → reskilling pathway, with every role and skill linked to the UN SDGs.

> **Human-centred:** this tool supports human career decisions. It does not replace human judgement and never makes final hiring, selection or promotion decisions.

## Who it is for

- Working adults at risk of job displacement
- Fresh graduates and career switchers
- HR / L&D managers (team mode)
- TVET and university career centres (batch mode)

## Quick start

```bash
git clone <this-repo-url>
cd <repo-folder>
pip install -r requirements.txt
streamlit run appnewver.py
```

Requires Python 3.9+. The app opens at `http://localhost:8501`.

Keep these files in the same folder as the app:

| File | Purpose |
|---|---|
| `appnewver.py` | Main Streamlit app |
| `ai_jobs_market_2025_2026.csv` | Open job-market dataset (see Data sources) |
| `trends_cache.json` | Cached arXiv signals, used when the live feed is unavailable |
| `requirements.txt` | Python dependencies |

## How the 6 must-have features are delivered

| # | Feature | Implementation |
|---|---|---|
| 1 | Skills profile intake | Form (current role, comma-separated skills), optional CV upload (PDF / DOCX / TXT) with automatic skill detection, and a short potential questionnaire (weekly study hours, learning style, willingness to learn) |
| 2 | AI-trend signal layer | (a) Job-posting dataset: share of each role and skill in 2025 vs 2026 postings drives the Future Skills Radar (rising / cooling). (b) Live arXiv cs.AI RSS feed, with source and fetch time shown in the sidebar, and a local cache as fallback |
| 3 | Future-role matching | Match score = skill coverage + background relevance (weights adjustable). Each role shows matched skills, missing skills (skills gap), number of postings, demand score and trend status |
| 4 | Personalised reskilling pathway | Ordered plan built from the user's missing skills (rising skills first), with estimated hours, estimated weeks from the user's weekly study hours, and free / low-cost resources. Includes progress checkboxes and badges |
| 5 | SDG mapping | All 17 SDGs. Each role and skill is tagged to at least one SDG; each recommendation shows how the career path contributes to the goals. An SDG coverage table and a regional SDG view are included |
| 6 | Handling uncertainty | Three scenarios (slow adoption / moderate change / rapid disruption) with an uncertainty range, clearly labelled as estimates. Multipliers and range are adjustable in the sidebar |

## Extra features

- **Team / batch mode** for HR and career centres: upload a CSV of members (template provided) to see a workforce skills-gap heatmap and regional SDG contribution
- **Automatic re-planning:** the app compares recommendations with and without trend signals and shows when the ranking changes
- **Fairness check:** option to match on skills only, plus a table showing how scores change across different backgrounds
- **Multi-language:** English, Bahasa Malaysia, 中文
- **Low-bandwidth mode:** no charts and no live fetch, uses cached data only
- **Learner motivation:** progress tracking and skill badges

## Data sources

- **Job-market data:** [Kaggle – AI Jobs Market 2025-2026](https://www.kaggle.com/datasets/alitaqishah/ai-jobs-market-2025-2026-salaries)
- **AI research signals:** arXiv cs.AI RSS feed
- **Learning resources:** public links (Kaggle Learn, Google Machine Learning Crash Course, DeepLearning.AI, Elements of AI, Coursera AI For Everyone)

Only public, open or synthetic data is used. No real personal data or real CVs are used; sample members are synthetic.

## AI disclosure and guardrails

- **No large language model (LLM) is used.** Role matching, the trend radar, SDG mapping and learning plans are computed from rules and public data.
- Every recommendation shows the source of its data (dataset and number of postings, arXiv signals with fetch time).
- The system does not invent jobs, courses or statistics. When data is missing, it says so (for example, scenarios are only shown when the dataset has a growth rate).
- CV files are processed in memory for the current session only and are not stored. Please upload only synthetic / sample CVs.

## Known limitations and risks

- **Small samples:** the 2026 data covers only part of the year and each role has a limited number of records, so the radar shows trend signals, not forecasts.
- **Static dataset:** the Kaggle CSV is a snapshot. The updatable part of the trend layer is the arXiv feed.
- **Light trend weighting:** arXiv signals use keyword matching on paper titles and have a small, bounded effect on ranking. A stronger source (for example, public job-posting feeds) is the next step.
- **Rule-based mappings:** SDG tags and resource suggestions are rule-based, and the resource list is limited. Skills without a matching resource fall back to a general course.
- **Scenario multipliers** are assumptions set by the team, not model outputs.

## Team

- Team name: _<add here>_
- Members: _<add here>_
