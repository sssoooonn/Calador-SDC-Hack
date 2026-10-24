| Field                  | Details                                                                                                                |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Team Name**          | Calador                                                                                                                |
| **Team Domain**        | Domain 1                                                                                                               |
| **SDG Track (1-17)**   | SDG 8 (Decent Work & Economic Growth), SDG 4 (Quality Education), SDG 10 (Reduced Inequalities), SDG 9 (Industry, Innovation & Infrastructure) |
| **Team Leader**        | Soon Yen Ling                                                                                                          |
| **University**         | TARUMT, UTAR                                                                                                           |
| **Number of Members**  | 4                                                                                                                      |

## Links

| Resource          | Link                                                                           |
| ----------------- | -------------------------------------------------------------------------------|
| GitHub Repository | https://github.com/sssooonn/Calador-SDC-Hack                                   |
| Replit Project    | https://calador-sdc-hack.replit.app                                            |
| Live Demo         |                                                                                |
| RunPod Endpoint   | N/A                                                                            |
| Slide Deck        | https://www.canva.com/design/DAHY534_36s/ZufM7Ieu6j9eMtLVq6_O7A/edit           |
| Demo Video        |                                                                                |


# Calador – AI Career & Skills Navigator

A proof-of-concept web app for the **Future-Ready Workforce Domain**. It takes a user from "who I am today" to "where I can be in the AI era": profile → future skills radar → ranked future roles → reskilling pathway, with every role and skill linked to the UN SDGs.

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

Requires Python 3.9+ and a recent version of Streamlit. The app opens at `http://localhost:8501`.

`requirements.txt` should contain:

```
streamlit
pandas
numpy
altair
feedparser
pypdf
python-docx
```

Keep these files in the same folder as the app:

| File | Purpose |
|---|---|
| `appnewver.py` | Main Streamlit app |
| `ai_jobs_market_2025_2026.csv` | Open job-market dataset (see Data sources) |
| `trends_cache.json` | Cached arXiv signals, used when the live feed is unavailable (created automatically) |
| `live_jobs_cache.json` | Cached live job ads, used when the live job source is unavailable (created automatically) |
| `requirements.txt` | Python dependencies |


## How to run

### Option A: Live app (no setup)

Open the deployed app: **https://calador-sdc-hack.replit.app**

### Option B: Run on Replit

1. Open the Replit project (or import this repo via **Create Repl → Import from GitHub**).
2. Make sure `appnewver.py`, `ai_jobs_market_2025_2026.csv` and `requirements.txt` are in the project root.
3. Click **Run**. Replit installs the dependencies from `requirements.txt` and starts the app with:
   ```bash
   streamlit run appnewver.py --server.address 0.0.0.0 --server.port 8080
   ```
4. The app opens in the Replit preview pane. Use **Open in new tab** for a full-page view.

### Option C: Run locally

See **Quick start** above.

> No API keys or secrets are needed. The live data sources (arXiv RSS, Arbeitnow API) are free and keyless. If they are unreachable, the app falls back to the cached JSON files, or you can turn on **Low-bandwidth mode**.

## How the 6 must-have features are delivered

| # | Feature | Implementation |
|---|---|---|
| 1 | Skills profile intake | Drop-down for current job / field of study, comma-separated skills, optional CV upload (PDF / DOCX / TXT) with automatic skill detection, an optional SDG preference (multi-select), and a short potential questionnaire (weekly study hours, learning style, willingness to learn). The questionnaire answers change the learning plan and the role ranking (see feature 4) |
| 2 | AI-trend signal layer | (a) Job-posting dataset: share of each role and skill in 2025 vs 2026 postings drives the Future Skills Radar (rising / cooling). (b) Live arXiv cs.AI RSS feed. (c) Live job ads from the Arbeitnow public API: the share of recent ads that mention each skill. Source and fetch time are shown for every live signal, and local caches are used as fallback |
| 3 | Future-role matching | Match score = 90% skill coverage + 10% background relevance (background can be switched off in the sidebar). Each role shows matched skills, missing skills (skills gap), number of postings, demand score and trend status. Trend signals, SDG preference and the questionnaire only fine-tune the ranking and never change the match score |
| 4 | Personalised reskilling pathway | Ordered plan built from the user's missing skills (rising skills first), with estimated hours, estimated weeks from the user's weekly study hours, and free / low-cost resources. Weekly study hours set how many courses are included, learning style changes the order of resources and the project step, and willingness to learn changes how much trend signals matter. Skills with no matching resource are listed honestly instead of being given an invented course. Includes progress checkboxes and badges |
| 5 | SDG mapping | All 17 SDGs. Each role and skill is tagged to at least one SDG; each recommendation shows how the career path contributes to the goals. Users can pick the SDGs they care about, which boosts related roles in the ranking. An SDG coverage table and a regional SDG view are included |
| 6 | Handling uncertainty | Three scenarios (slow adoption / moderate change / rapid disruption) with an uncertainty range, clearly labelled as estimates. Multipliers and range are adjustable in the sidebar |

## Extra features

- **Team / batch mode** for HR and career centres: upload a CSV of members (template provided) to see a workforce skills-gap heatmap and regional SDG contribution
- **Automatic re-planning:** the app compares recommendations with and without trend signals and shows when the ranking changes
- **Fairness check:** option to match on skills only, plus a table showing how scores change across different backgrounds
- **Live job-market signal:** a dedicated panel compares the share of each skill in live job ads with the dataset's 2026 share
- **Multi-language:** English, Bahasa Malaysia, 中文
- **Low-bandwidth mode:** no charts and no live fetch, uses cached data only
- **Learner motivation:** progress tracking and skill badges

## Data sources

- **Job-market data:** [Kaggle – AI Jobs Market 2025-2026](https://www.kaggle.com/datasets/alitaqishah/ai-jobs-market-2025-2026-salaries)
- **AI research signals:** arXiv cs.AI RSS feed
- **Live job ads:** [Arbeitnow](https://www.arbeitnow.com/) public job-board API (free, no key)
- **Learning resources:** public links (Kaggle Learn, Google Machine Learning Crash Course, DeepLearning.AI, Elements of AI, Coursera AI For Everyone)

Only public, open or synthetic data is used. No real personal data or real CVs are used; sample members are synthetic.

## AI disclosure and guardrails

- **No large language model (LLM) is used.** Role matching, the trend radar, SDG mapping and learning plans are computed from rules and public data.
- Every recommendation shows the source of its data (dataset and number of postings, arXiv signals and live job ads with fetch time).
- The system does not invent jobs, courses or statistics. When data is missing, it says so (for example, scenarios are only shown when the dataset has a growth rate, and skills without a matching resource are listed as such).
- CV files are processed in memory for the current session only and are not stored. Please upload only synthetic / sample CVs.

## How we used Replit

Replit was our single environment for building, debugging and deploying Calador.

| Stage | How we used Replit |
|---|---|
| **Build** | Wrote and previewed the Streamlit app (`appnewver.py`) in the browser editor, with the live preview pane to test each feature as we built it. Dependencies were managed through `requirements.txt`. |
| **Solve problems** | Used the Replit console and logs to find and fix errors ). Replit's built-in AI assistance was used to help us debug and fix issues. |
| **Deploy** | Published the app with Replit Deployments so it runs at a public URL without local setup: **https://calador-sdc-hack.replit.app**. |


## Known limitations and risks

- **Small samples:** the 2026 data covers only part of the year and each role has a limited number of records, so the radar shows trend signals, not forecasts.
- **Static dataset:** the Kaggle CSV is a snapshot. The updatable parts of the trend layer are the arXiv feed and the live job ads.
- **Live job source is not the Malaysian market:** Arbeitnow lists mostly European / German-speaking tech jobs (including remote). It is used as a live demand signal only, with a small, bounded effect on ranking and skill order.
- **Keyword matching:** arXiv signals match keywords in paper titles, and live job signals match skill names in ad text, so both are rough signals.
- **CV detection:** the system only recognises skill names that appear in the dataset, and it cannot read scanned (image-only) PDFs. Users can add skills manually.
- **Rule-based mappings:** SDG tags and resource suggestions are rule-based, and the resource list is limited.
- **Assumptions set by the team, not model outputs:** scenario multipliers, and the questionnaire rules (number of courses per weekly-hours range, ranking weights for willingness to learn, project hours).

## Team

- Team name: Calador
- Members: Soon Yen Ling , Chang Hui Yee , Soon Yen Yao , Soon Jiun Hau
