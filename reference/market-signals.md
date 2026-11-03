# Market signals and alignment contract

> Lab-wide market alignment contract, revision 2.
> What hiring managers, execs, and partners measurably value; what the lab
> collects to prove it; how roadmaps, resumes, and positioning stay aligned.
>
> **Last scan:** 2026-11-02 (DEV-125 monthly pass 2026-11-01 +
> browser-automation evidence 2026-11-02; baseline 2026-10-28)
> **Driver:** Linear DEV-125 (living research ticket)
> **Decay policy:** every fact carries a date + source. Facts older than 2
> quarters are stale until re-verified by the next DEV-125 pass.

## Status

Living document. Does NOT self-update. Refresh path:

1. DEV-125 pass reruns the bounded web scan (3-6 queries: hiring keywords,
   exec-valued engineering metrics, AI/agentic market numbers).
2. Findings updated in place in DEV-125; decayed claims marked
   `(stale, replaced by X)`.
3. Deltas synced here and into Linear doc
   "Contribution Ledger: Conventions + Stats" -> Market signal lens.
4. Cadence: monthly while applications/partnerships are active, quarterly
   otherwise.

## Verified signals (baseline 2026-10-28, refreshed 2026-11-01)

### Metrics that reviewers and execs check

| Signal                    | Verified benchmark / adoption                                                                                                    | Source                            |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| Deploy frequency          | Elite >1 deploy/service/day                                                                                                      | LinearB 2025 (not re-verified)    |
| Cycle / lead time         | Elite <26h                                                                                                                       | LinearB 2025 (not re-verified)    |
| Change failure rate       | Elite <1%                                                                                                                        | LinearB 2025 (not re-verified)    |
| MTTR                      | Elite <6h                                                                                                                        | LinearB 2025 (not re-verified)    |
| AI amplifies the system   | AI adoption 90% (+14 pts YoY); >80% perceive productivity gain; 59% positive code quality; 30% trust output little or not at all | DORA 2025 (2025-09-23, ~5,000)    |
| AI-era bottleneck moved   | PR throughput +~20% YoY; defect ratio -16.9%; AI time saved 3.9 -> 6.2 h/dev/week; review turnaround declined                    | DX 2026 benchmarks (2026-07-21)   |
| AI ROI attainment         | 19% of CIOs met or exceeded AI ROI goals; 47% run formal AI KPIs; top metric operational efficiency 40%                          | State of the CIO 2026 (n=911)     |
| SPACE framework           | >50% of dev teams; top productivity frame 2025                                                                                   | Atlassian DevEx (not re-verified) |
| DORA + satisfaction blend | deploy freq, perf, lead time, satisfaction each ~34-35% of orgs                                                                  | JetBrains DevEx (not re-verified) |
| Revenue per Engineer      | Median $892K; top quartile $1.5M+ (2026 DX release did not refresh RpE)                                                          | DX Core 4 (2025-04-09)            |
| AI impact measures        | time saved, PR throughput, CFR, engaged users, innovation rate                                                                   | DX survey of 18                   |

### Exec pain: unclear AI ROI

- ~2/3 of software firms deployed genAI; only 10-15% productivity lift;
  gains evaporate when saved time is not redirected (Bain 2025).
- Coding is ~25-35% of idea-to-launch time: SDLC-wide AI beats codegen-only
  (Bain 2025).
- Unclear ROI is the top CIO/CTO adoption hurdle; fix pattern = scorecards +
  developer satisfaction (BCG 2025). Only 19% report AI ROI goals met (State
  of the CIO 2026).

### Keyword watchlist (growth-verified, 2026-11-01)

| Keyword                                            | Verified growth                                                                                 |
| -------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| AI/ML tech postings                                | +88% YoY vs +17% all tech postings (Dice Sep 2026; Lightcast, 7M+ US postings)                  |
| Agentic AI / AI agents / Responsible AI / AI infra | each 200%+ YoY; employers now name tools (Dice Sep 2026)                                        |
| GenAI requirement in recruiter searches            | 5.37% -> 9.44% of 120K+ searches Q3 2025 -> Q3 2026; AI-agent requirement 3.75x (Pin)           |
| AI engineering                                     | #1 fastest-growing skill; AI-literacy postings +70% YoY (LinkedIn Skills on the Rise 2026)      |
| AI engineer / GenAI engineer postings              | +255% / +197% YoY (DataCamp State of AI Careers 2026)                                           |
| MCP server                                         | official registry 38,977 (2026-10-04) -> 53,637 (2026-10-31); 2,770 of 3,745 scanned maintained |
| Python in AI-company JDs                           | 27.9% of 15,314 JDs; LLMs 15.5%; Agents 14.8%; Evals 3.8% (AI Hiring Index, 2026-11-01)         |
| Agentic-systems roles                              | median salary $225K (frontierroles.com; not re-verified 2026-11-01)                             |

Stale, replaced 2026-11-01: Dice 2025 "+2043% AI agents, +608% edge
intelligence, +475% RAG, 36% of US postings require AI skills"; MCP "~2000
registry entries, +407%". Edge intelligence has no 2026 verification.

Adjacent vocabulary to use: evals + LLM observability, context engineering,
AI safety + guardrails, platform engineering, edge/serverless, FinOps,
SDLC-wide AI, Selenium / WebDriver BiDi, Tkinter, API integration, Python
process automation, UI automation (RPA), computer-use agents.

### Browser automation: state of the art (2026-11-02)

Selenium project facts (primary sources: selenium.dev, SeleniumHQ/selenium):

- Cadence: 4.52 (2026-10-29) and 4.51 (2026-10-09); two-week release train
  (TLC 2026-09-03). Python 3.15 supported since 4.51.
- WebDriver BiDi: W3C bidirectional protocol co-authored by Selenium and the
  browser vendors; streams network, console, and JS-error events over a
  WebSocket; cross-browser replacement for CDP. Python enables it with
  `options.enable_bidi = True`; 4.52 removed sleep-polling on the BiDi socket
  (faster command round-trips); web extensions install from the driver.
- CDP: Firefox CDP removed in 4.29 (2025); Chrome CDP kept 3 versions deep
  (v154-v156 in 4.52); TLC deferred the CDP deprecation timeline pending
  usage data (2026-09-03).
- Selenium Manager: built-in driver and browser provisioning; 4.52 validates
  TLS certificates; being split into its own package.
- Grid: file upload and download forwarding for Docker, Kubernetes, and relay
  sessions (PR #17914, 2026); Helm chart maintained.
- Roadmap: 5.0 milestone = async event-based high-level API in every binding,
  Selenium Manager stable, BiDi internals private, backward compatible; 6.0 =
  every classic command implemented over BiDi; release charter PR #17717.

Competitive position (practitioner surveys split from posting counts):

| Measure                                     | Selenium                | Playwright | Source (date)                                         |
| ------------------------------------------- | ----------------------- | ---------- | ----------------------------------------------------- |
| Extensive use, all developers (n=10,604)    | 12.0%                   | 24.9%      | Stack Overflow Developer Survey 2026 (2026-10-06)     |
| PyPI downloads, last 30 days                | 28.0M                   | 97.0M      | pypistats.org (2026-11-02)                            |
| US QA postings naming the tool (n=552)      | 47%                     | 46%        | Codecaf (2026-10-31)                                  |
| US postings that name a framework (n=439)   | 62%                     | 64%        | AssertHired, 7,040 postings 2026-09-15 to 2026-11-02  |
| Canada / UK share of framework-naming posts | 77% / 33%               | 40% / 82%  | AssertHired (2026-11-02)                              |
| Companies whose postings name it            | 8,888 (1,985 confirmed) | n/a        | jobspipe.dev, 29,289 postings (2026-09-25)            |
| JS developers only                          | 10%                     | 50%        | State of JavaScript 2025 testing (secondary citation) |

Caveats: registry download counts are increasingly inflated by non-testing
AI-agent use (OSF empirical study, 2026-10-22); Selenium weekly posting volume
eased 1,117 -> 779 across Aug-Nov 2026 (GetUHired); the recycled "TestGuild
45.1% Playwright vs 22.1% Selenium" figure is a 2024 TestGuild number
republished as 2026 data; do not cite it.

Agentic frontier (where the skill is heading):

- Gartner: "by 2027, 60% of RPA vendors will include computer-use
  capabilities to augment UI interactions" (MQ RPA, 2025-06-23); follow-up
  note "Decoding Computer Use Agents: The Future of RPA" (2026-01-08).
- WebMCP: Chromium 146 early preview (2026-02-10), origin trial from Chrome
  149; sites expose structured tools to agents instead of raw DOM actuation.
  Locator brittleness, the main Selenium maintenance cost, is the target.
- `@playwright/mcp` is the top MCP package at 28M downloads/month (DEV-125,
  2026-10-31): browser automation is now agent substrate, not only test glue.
- Human skill shifts to orchestration and validation: BiDi event handling,
  exception design, evidence capture (screenshots, network logs), and
  deciding what gets automated (PractiTest: only 19.9% use AI for risk
  identification).

### Where UI automation pays: measured outcomes

Numbers an automation developer can be held to; use them as baselines when
framing `## Impact`.

| Outcome                       | Measured result                                                                                                                                                       | Source (date)                                              |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Capacity, government-wide     | >1.4M hours of low-value work removed; ~1,000 automations in production; >1M hours created in FY21                                                                    | Federal RPA CoP, State of Federal RPA v2.0 (2021-12-29)    |
| Capacity, one program         | GSA: 70 automations, 200K+ hours annualized capacity                                                                                                                  | State of Federal RPA v1.0 (2020)                           |
| Capacity + cost, one bureau   | Treasury Fiscal Service: 104 bots since 2020, 186,000 employee hours, ~$13.6M saved                                                                                   | Federal News Network (2024-10)                             |
| Cycle time                    | monthly management report 5-8 days -> 1 hour; expense report 3 h/day -> 10 min; manual-entry errors eliminated                                                        | Deloitte Brazil RPA case, IBM case study                   |
| Cost and payback              | beyond-pilot orgs achieved -32% cost (24% in 2020); expected -31% over 3 yrs; pilot payback 16 -> 22 months as scope grew; >50% never calculated cost reduction       | Deloitte intelligent automation survey 2022 (2021/22 data) |
| Scale and AI premium          | at-scale automators: payback 9 months vs 15 for pilots; RPA+AI revenue +9% vs RPA-only +3%                                                                            | Deloitte 2019 survey, Deloitte Review 26 (2020-01)         |
| Gen AI in quality engineering | ~19% productivity gain across test design, requirements analysis, script maintenance; automation coverage averages one-third of test cases; AI non-adopters 4% -> 11% | World Quality Report 2025-26 (2,000 execs, 23 countries)   |
| Market size                   | RPA revenue $3.8B in 2024, +18% YoY                                                                                                                                   | Gartner MQ RPA (2025-06-23)                                |
| Failure mode                  | up to half of RPA adopters missed expected ROI or failed to scale beyond early wins                                                                                   | IBM "The transformational power of RPA"                    |
| Test automation ROI           | strong automation + CI/CD: 86% faster releases, 71% less defect leakage, 58% ROI within 6 months (n=2,751)                                                            | TestRail 2025 (secondary citation; verify next pass)       |
| Measurement trap              | 56% of QA teams measured on test coverage, 4.5% on NPS                                                                                                                | PractiTest State of Testing 2026                           |

Context on why automation reqs stress validation, logging, and exception
handling: the Boston Fed CIO framed RPA for compliance-heavy work that must
run "error and bias free and consistently" (2018; dated, context only).

Decision rule, Selenium vs alternatives:

- UI is the only integration surface (vendor portal, legacy intranet, no API):
  Selenium or RPA; Gartner defines RPA as UI emulation "where APIs are limited
  or unavailable".
- Existing Python/Java/C# estate on Grid + Jenkins: keep Selenium; migration
  ROI is usually negative for stable suites.
- Cross-browser evidence for compliance: BiDi is the W3C path.
- Greenfield JS/TS or agent tooling: Playwright is the default.

Automation-work impact metrics (extend the collection contract below): hours
of capacity created per year; process cycle time before/after; exceptions or
manual touches per 1,000 runs; job success rate and MTTR; payback months.

### Market position shift

Builders -> Orchestrators. AI engineer responsibility share (Northzone):
prompt/retrieval optimization 90%, model eval 80%, LLM stack
(RAG/chains/agents) 70%, fine-tuning 50%, infra 35%, training models 5%.
DevArts Lab operates in the orchestration tier.

## Collection contract (what every ledger entry must carry)

`## Impact` numbers draw from this set, not ad-hoc counts:

- deploys/week, lead time, cycle time
- change failure rate, MTTR, uptime, p99 latency
- review turnaround, PR revert rate (DX 2026: the AI-era bottlenecks)
- tests added/passing, coverage delta
- endpoints live, users served, records processed
- cost saved or unit-cost basis (RpE proxy where estimable)
- time saved vs manual baseline (AI ROI narrative)
- automation work: hours of capacity/year, cycle time before/after,
  exceptions per 1,000 runs, payback months

`## Evidence` is mandatory: every number links to a click-verifiable source
(commit SHA, PR, live URL, dashboard).

Work descriptions tag market vocabulary on the way in (agentic AI, MCP
server, RAG, evals, guardrails, platform engineering, edge/serverless,
FinOps, UI automation, Selenium / WebDriver BiDi, API integration, Python
process automation) so label-and-keyword queries surface the right bullets.

## Alignment rules (bind every lab product + pitch)

1. Position as SDLC-wide orchestration (plan, build, test, deploy, observe),
   never codegen-only. Matches where Bain says real returns come from.
2. Lead every product story with a quantified scorecard: cadence, failure
   rate, time saved, cost basis. This is the artifact execs say is missing.
3. Resume/ledger framing maps each bullet to DORA/SPACE/Core 4 vocabulary
   first, proprietary terms second.
4. Vision/mission framing: healthy growth = measurable leverage per
   engineer, not headcount. We sell orchestration and verified impact.
5. New roadmap items check the keyword watchlist: does the item compound an
   in-demand signal or chase a decaying one? Note the answer in the issue.
6. Automation work is framed as integration (UI when no API, API when one
   exists) with capacity hours and cycle-time deltas, never as "scripting".

## Source register (2026-10-28)

Dice AI Hiring Guide 2025 | LinearB 2025 Software Engineering Benchmarks |
DX Core 4 Revenue-per-Engineer benchmarks | DX "How 18 companies measure AI
impact" | Bain "From Pilots to Payoff" 2025 | BCG "AI-Enabled Engineering
Excellence" 2025 | Northzone "On The Pulse: AI Engineer Hiring" | MCP
anniversary post 2025-11 | frontierroles.com agentic salary data |
InfoWorld "9 AI development skills" | Atlassian + JetBrains DevEx surveys.

## Source register additions (2026-11-01, DEV-125 monthly pass)

DORA 2025 State of AI-assisted Software Development | DX 2026 benchmarks |
Foundry State of the CIO 2026 | Dice Tech Job Report Sep 2026 | Pin
recruiter-search data Q3 2026 | LinkedIn Skills on the Rise 2026 (via CIO
Dive) | DataCamp State of AI Careers 2026 | AI Hiring Index | ProtocolProbe
and Major Labs MCP registry counts | Gartner agentic AI Hype Cycle 2026.
URLs in Linear DEV-125 Findings.

## Source register additions (2026-11-02, browser automation)

Recruiter outreach is not tracked here; contact and req material stays in
career-dev (D14).

| Topic                                       | URL                                                                                                                         |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Codecaf QA hiring statistics (552 postings) | <https://codecaf.com/research/qa-hiring-statistics/>                                                                        |
| AssertHired QA job market (7,040 postings)  | <https://www.asserthired.com/qa-jobs/market>                                                                                |
| GetUHired Selenium hiring trends            | <https://getuhired.co/insights/tech/selenium/>                                                                              |
| jobspipe Selenium employers                 | <https://jobspipe.dev/technologies/selenium>                                                                                |
| Stack Overflow 2026, code testing tools     | <https://survey.stackoverflow.co/2026/technology/data/code-test>                                                            |
| Stack Overflow 2026, languages              | <https://survey.stackoverflow.co/2026/technology/data/languages>                                                            |
| pypistats selenium / playwright             | <https://pypistats.org/packages/selenium> / <https://pypistats.org/packages/playwright>                                     |
| Selenium 4.52 release                       | <https://www.selenium.dev/blog/2026/selenium-4-52-released/>                                                                |
| Selenium 4.51 release                       | <https://www.selenium.dev/blog/2026/selenium-4-51-released/>                                                                |
| Selenium TLC meeting 2026-09-03             | <https://www.selenium.dev/meetings/2026/tlc-09-03/>                                                                         |
| Selenium milestones (5.0, 6.0)              | <https://github.com/SeleniumHQ/selenium/milestones>                                                                         |
| Selenium 5 release charter                  | <https://github.com/SeleniumHQ/selenium/pull/17717>                                                                         |
| WebDriver BiDi documentation                | <https://www.selenium.dev/documentation/webdriver/bidi/>                                                                    |
| OSF browser-automation adoption study       | <https://doi.org/10.17605/osf.io/atnp4>                                                                                     |
| Gartner MQ RPA 2025                         | <https://www.gartner.com/en/documents/6632834>                                                                              |
| Gartner computer-use agents note            | <https://www.gartner.com/en/documents/7321230>                                                                              |
| WebMCP early preview / origin trial         | <https://developer.chrome.com/blog/webmcp-epp> / <https://developer.chrome.com/docs/ai/webmcp>                              |
| State of Federal RPA v2.0                   | <https://digital.gov/s3/files/m-files/state-of-federal-rpa-report-12-2021.pdf>                                              |
| State of Federal RPA v1.0                   | <https://digital.gov/s3/files/m-files/state-of-federal-rpa.pdf>                                                             |
| Fiscal Service intelligent automation       | <https://federalnewsnetwork.com/automation/2024/10/for-fiscal-service-intelligent-automation-transforms-federal-workflows/> |
| Deloitte intelligent automation 2022        | <https://www.deloitte.com/content/dam/assets-shared/legacy/docs/insights/2022/DI_Automation-with-intelligence.pdf>          |
| Deloitte Review 26, 2019 survey             | <https://www.deloitte.com/content/dam/assets-shared/legacy/docs/insights/2022/DI_DR26-Automation-with-intelligence.pdf>     |
| World Quality Report 2025-26                | <https://www.capgemini.com/insights/research-library/world-quality-report-2025-26/>                                         |
| Deloitte Brazil RPA case (IBM)              | <https://www.ibm.com/downloads/documents/us-en/107a02e949c8f57d>                                                            |
| IBM transformational power of RPA           | <https://www.ibm.com/resources/automate/power-of-rpa>                                                                       |
| PractiTest State of Testing 2026            | <https://www.practitest.com/state-of-testing/>                                                                              |
| Postman State of the API 2025               | <https://www.postman.com/state-of-api/2025/>                                                                                |
| Python Developers Survey 2024               | <https://lp.jetbrains.com/python-developers-survey-2024/>                                                                   |
| Boston Fed CIO on RPA (2018)                | <https://www.bostonfed.org/news-and-events/news/2018/anderson-robotic-process-automation.aspx>                              |
