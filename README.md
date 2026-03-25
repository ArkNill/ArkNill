## About

Backend engineer with 6+ years building data-intensive systems — from SQL tuning across **6 database engines** to deploying local LLM inference pipelines on bare metal.

I believe the next wave of useful software won't come from training bigger models, but from **building better plumbing around them** — reliable extraction, structured search, safety guardrails, and pipelines that run without cloud API keys.

Currently building [QuartzUnit](https://github.com/QuartzUnit): composable Python tools that let AI agents collect, extract, search, and monitor data — entirely locally.

---

## Currently Working On

- **QuartzUnit ecosystem** — 10 Python packages on PyPI, each solving one step in the LLM data pipeline
- **Fact-checking pipeline** — automated claim extraction → evidence collection → verdict generation (production at 83.6% effective accuracy)
- **Large-scale web collection** — 800K+ quality articles across 115 domains, legal RSS-only approach
- **Air-gapped LLM infrastructure** — building data pipelines and test datasets that work identically in online and offline environments

---

## What I Build

<table>
<tr>
<td width="50%" valign="top">

### Data & AI Pipelines

I focus on making LLM pipelines work **in both online and air-gapped environments** — same code, same quality, no cloud dependency. Having delivered CUBE (BI/OLAP), DW/DM builds, and custom analytics to government and public sector clients on closed networks, I know what "no internet" really means for AI deployment.

The tools I build — data collection, content extraction, semantic search, fact-checking — are designed to produce **local test datasets** from legally collected public sources (RSS, public APIs). This lets teams validate LLM pipelines on realistic data before deploying to restricted environments.

`Python` `vLLM` `PostgreSQL` `Qdrant` `Neo4j` `Redis`

</td>
<td width="50%" valign="top">

### Full-stack Services

Backend APIs with Spring Boot and FastAPI, web dashboards with Next.js, Android apps with Jetpack Compose, and cross-platform mobile with React Native.

I design from the database schema up — performance-tuned queries across PostgreSQL, Oracle, MariaDB, MSSQL, DB2, and Netezza. When the bottleneck is the query, I fix the query. When the bottleneck is the schema, I fix the schema.

`FastAPI` `Spring Boot` `Next.js` `React Native` `Kotlin` `JPA`

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

### Built with these tools

These projects use QuartzUnit packages as dependencies — real pipelines, not demos:

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
| **Online + Offline** | Pipelines validated in both open and air-gapped environments |

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
