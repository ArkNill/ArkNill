## About

Backend engineer with 6+ years building data-intensive systems — SQL-native tuning across **6 heterogeneous databases** (PostgreSQL, Oracle, MariaDB, MSSQL, DB2, Netezza), full-stack from backend to mobile, and now building AI service pipelines end-to-end.

I believe the next wave of useful software won't come from training bigger models, but from **building better plumbing around them** — reliable extraction, structured search, safety guardrails, and pipelines that run without cloud API keys.

Currently building [QuartzUnit](https://github.com/QuartzUnit): composable Python tools that let AI agents collect, extract, search, and monitor data — entirely locally.

---

## Currently Working On

- **Mirror Agent** — local autonomous AI agent with custom ReAct pipeline, RAG (Qdrant + Neo4j), persistent memory, and 2-tier LLM fallback. No framework, no cloud. Runs entirely on-premise.
- **Forge** — multi-source data refinement into LLM-ready warehouses. Any domain, any source — news, blogs, enterprise back-data, legacy DB migrations. Includes fact-checking at 83.6% production accuracy.
- **QubicAI** — automated data mart generation + natural language → SQL. Turns Forge warehouses into queryable marts that LLMs can use directly.
- **QuartzUnit** — personal data asset platform. Consumption/production knowledge archiving + AI labeling + mobile app. Building toward a personal data marketplace.
- **QuartzUnit OSS** — 10 Python packages on PyPI extracted from the above projects. The composable tool layer that powers the ecosystem.

---

## What I Build

<table>
<tr>
<td width="50%" valign="top">

### Data & AI Pipelines

LLM pipelines that work identically **online and offline** — collection → extraction → RAG → fact-checking, all on local inference.

- Autonomous AI agent with RAG (Qdrant + Neo4j), persistent memory, and custom ReAct pipeline
- Automated fact-checking: claim extraction → tiered evidence search → verdict generation
- 800K+ articles collected, indexed, and searchable across 115 domains

`Python` `vLLM` `PostgreSQL` `Qdrant` `Neo4j` `Redis`

</td>
<td width="50%" valign="top">

### Full-stack & Data Engineering

6 years delivering DW/DM, BI/OLAP, and analytics to government and enterprise clients — often on air-gapped networks. Cross-DB migrations, query tuning, report automation.

- LLM chatbot → natural language to BI dashboards (5-step UI → 1 sentence)
- Video analytics with PGVector semantic search + LLM-powered metadata structuring
- Mobile + web: Next.js dashboards, Kotlin/Compose Android, React Native

`FastAPI` `Spring Boot` `Next.js` `Kotlin` `JPA` `React Native`

</td>
</tr>
</table>

---

## QuartzUnit — LLM-native Tool Ecosystem

Most AI agent frameworks give you an orchestrator but expect you to figure out the I/O yourself. QuartzUnit is the I/O layer — **10 focused tools** that each solve one problem well, designed to be chained together.

Every tool ships with three interfaces: CLI for scripting, async Python API for integration, and MCP server for AI agent consumption. Zero cloud dependency — everything runs on your machine.

```
Collect          Extract          Search           Monitor          Guard
─────────        ─────────        ─────────        ─────────        ─────────
feedkit    ───→  markgrab   ───→  embgrep    ───→  diffgrab         agent-action-policy
(RSS/Atom)       (HTML/PDF/       (semantic)       (web change      agent-loop-guard
                  YouTube)                          tracking)       llm-degen-guard
                 docpick
                 (OCR→JSON)       browsegrab ───→  snapgrab
                                  (browser         (screenshot)
                                   agent)
```

### Why I built this

I needed these tools for my own data pipelines — collecting news from 444 RSS feeds, extracting article content for fact-checking, searching across collected documents by meaning, and monitoring pages for changes. Every tool started as a module in a private project, then got extracted into a standalone package when it became useful on its own.

The guard libraries (loop detection, degeneration detection, action policies) came from running autonomous agents that would occasionally get stuck in loops, produce garbage output, or try to access things they shouldn't. Rather than adding ad-hoc checks, I built proper detectors that any agent framework can use.

### Packages

| Package | What it does | PyPI | Tests |
|---------|-------------|------|------:|
| [markgrab](https://github.com/QuartzUnit/markgrab) | URL → LLM-ready markdown (HTML, YouTube, PDF, DOCX) | [![PyPI](https://img.shields.io/pypi/v/markgrab?style=flat-square)](https://pypi.org/project/markgrab/) | 114 |
| [docpick](https://github.com/QuartzUnit/docpick) | Schema-driven document OCR → structured JSON | [![PyPI](https://img.shields.io/pypi/v/docpick?style=flat-square)](https://pypi.org/project/docpick/) | 217 |
| [feedkit](https://github.com/QuartzUnit/feedkit) | RSS/Atom collection with 444 curated feeds | [![PyPI](https://img.shields.io/pypi/v/feedkit?style=flat-square)](https://pypi.org/project/feedkit/) | 34 |
| [browsegrab](https://github.com/QuartzUnit/browsegrab) | Token-efficient browser agent for local LLMs | [![PyPI](https://img.shields.io/pypi/v/browsegrab?style=flat-square)](https://pypi.org/project/browsegrab/) | 200 |
| [snapgrab](https://github.com/QuartzUnit/snapgrab) | URL → screenshot + metadata (Claude Vision optimized) | [![PyPI](https://img.shields.io/pypi/v/snapgrab?style=flat-square)](https://pypi.org/project/snapgrab/) | 29 |
| [diffgrab](https://github.com/QuartzUnit/diffgrab) | Web page change tracking with structured diffs | [![PyPI](https://img.shields.io/pypi/v/diffgrab?style=flat-square)](https://pypi.org/project/diffgrab/) | 89 |
| [embgrep](https://github.com/QuartzUnit/embgrep) | Local semantic search (embedding-powered grep) | [![PyPI](https://img.shields.io/pypi/v/embgrep?style=flat-square)](https://pypi.org/project/embgrep/) | 74 |
| [llm-degen-guard](https://github.com/QuartzUnit/llm-degen-guard) | LLM output degeneration detector | [![PyPI](https://img.shields.io/pypi/v/llm-degen-guard?style=flat-square)](https://pypi.org/project/llm-degen-guard/) | 55 |
| [agent-loop-guard](https://github.com/QuartzUnit/agent-loop-guard) | Agent infinite loop detection | [![PyPI](https://img.shields.io/pypi/v/agent-loop-guard?style=flat-square)](https://pypi.org/project/agent-loop-guard/) | 78 |
| [agent-action-policy](https://github.com/QuartzUnit/agent-action-policy) | Declarative action policies for AI agents | [![PyPI](https://img.shields.io/pypi/v/agent-action-policy?style=flat-square)](https://pypi.org/project/agent-action-policy/) | 69 |

**959 tests** across 10 packages · All MIT licensed · Korean + English documentation

### Showcase

End-to-end examples showing how QuartzUnit packages chain together:

| Project | Pipeline | What it does |
|---------|----------|-------------|
| [newswatch](https://github.com/QuartzUnit/newswatch) | feedkit → markgrab → embgrep → diffgrab | Collect RSS feeds, extract articles, build semantic search index, track changes |
| [watchdeck](https://github.com/QuartzUnit/watchdeck) | diffgrab → markgrab → snapgrab → guard trio | Monitor web pages for changes with visual diffs and safety guards |

---

## By the Numbers

| | |
|---|---|
| **6** | Database engines tuned in production (PostgreSQL, Oracle, MariaDB, MSSQL, DB2, Netezza) |
| **10** | Open-source Python packages on PyPI |
| **959** | Tests across the QuartzUnit ecosystem |
| **444** | Curated, verified RSS feeds in the feedkit catalog |
| **800K+** | Quality articles collected across 115 domains |
| **83.6%** | Fact-checking pipeline effective accuracy (production) |

---

## Tech Stack

**Languages**

![Python](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Java](https://img.shields.io/badge/-Java-007396?style=flat-square&logo=openjdk&logoColor=white)
![Kotlin](https://img.shields.io/badge/-Kotlin-7F52FF?style=flat-square&logo=kotlin&logoColor=white)
![TypeScript](https://img.shields.io/badge/-TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![SQL](https://img.shields.io/badge/-SQL-CC2927?style=flat-square&logo=databricks&logoColor=white)

**Backend & AI**

![FastAPI](https://img.shields.io/badge/-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Spring Boot](https://img.shields.io/badge/-Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![vLLM](https://img.shields.io/badge/-vLLM-FF6F00?style=flat-square&logo=lightning&logoColor=white)
![Qdrant](https://img.shields.io/badge/-Qdrant-DC244C?style=flat-square&logo=qdrant&logoColor=white)
![Neo4j](https://img.shields.io/badge/-Neo4j-4581C3?style=flat-square&logo=neo4j&logoColor=white)

**Database**

![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Oracle](https://img.shields.io/badge/-Oracle-F80000?style=flat-square&logo=oracle&logoColor=white)
![MariaDB](https://img.shields.io/badge/-MariaDB-003545?style=flat-square&logo=mariadb&logoColor=white)
![MSSQL](https://img.shields.io/badge/-MSSQL-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white)
![DB2](https://img.shields.io/badge/-DB2-052FAD?style=flat-square&logo=ibm&logoColor=white)
![Redis](https://img.shields.io/badge/-Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

**Frontend & Mobile**

![Next.js](https://img.shields.io/badge/-Next.js-000000?style=flat-square&logo=next.js&logoColor=white)
![React Native](https://img.shields.io/badge/-React_Native-61DAFB?style=flat-square&logo=react&logoColor=black)
![Jetpack Compose](https://img.shields.io/badge/-Jetpack_Compose-4285F4?style=flat-square&logo=jetpackcompose&logoColor=white)

**Infra**

![Docker](https://img.shields.io/badge/-Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/-GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Cloudflare](https://img.shields.io/badge/-Cloudflare-F38020?style=flat-square&logo=cloudflare&logoColor=white)
![Playwright](https://img.shields.io/badge/-Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white)
