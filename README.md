# Awesome AEO & SEO Tools [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Curated free and open-source tools for Answer Engine Optimization (AEO), Generative Engine Optimization (GEO), and technical SEO - covering audit, monitoring, infrastructure, content scoring, and statistical measurement. Every entry is free, open-source, or a Discovered Labs free tool; no SaaS vendor links.

Maintained by [Discovered Labs](https://discoveredlabs.com). For the research and papers behind these tools, see [awesome-aeo-seo](https://github.com/discoveredlabs/awesome-aeo-seo). For agent-native integrations and MCP servers, see [awesome-aeo-seo-agents](https://github.com/discoveredlabs/awesome-aeo-seo-agents).

## Contents

- [How AI Search Engines Work](#how-ai-search-engines-work)
- [All-in-One GEO/AEO Audit](#all-in-one-geoaeo-audit)
- [AI Visibility Monitoring and Brand Tracking](#ai-visibility-monitoring-and-brand-tracking)
- [Technical AEO Infrastructure](#technical-aeo-infrastructure)
- [Content Audit and Optimization](#content-audit-and-optimization)
- [SEO Research and Data Platforms](#seo-research-and-data-platforms)
- [Agent Skill Packages](#agent-skill-packages)
- [Measurement and Calculators](#measurement-and-calculators)
- [Related Lists](#related-lists)
- [Contributing](#contributing)

---

## How AI Search Engines Work

Reverse-engineered technical analysis of how ChatGPT, Google AI Overviews, AI Mode, and Gemini retrieve, rank, and synthesize content - and how their commercial infrastructure is built. Understanding the retrieval pipeline is the prerequisite for using any tool in this list effectively.

### Retrieval Mechanics

- [How AI Search Grounding Actually Works: Google vs OpenAI vs Anthropic](https://dejan.ai/blog/grounding/) - Same query, three platforms: Google retrieves 7 pages and cites all 7 (1:1), OpenAI retrieves 39 and cites 2 (20:1 filtering), Anthropic reads 14 and cites 9; the citation budget difference means tools measuring "AI brand visibility" across platforms are measuring structurally incompatible things - the operational prerequisite for interpreting multi-engine monitoring output correctly.

- [How ChatGPT Uses Reciprocal Rank Fusion for AI Citations](https://discoveredlabs.com/blog/how-chatgpt-uses-reciprocal-rank-fusion-for-ai-citations) - Covers ChatGPT's hybrid BM25 + vector retrieval pipeline fused via RRF with scoring formula `1/(rank+k)` at `k=60`; extracted code-level parameters (`rrf_alpha: 1`, `rrf_input_threshold: 0`) show that consistent mid-list presence across both retrieval methods outperforms a #1 ranking that appears in only one.

- [How Google AI Overviews Works](https://discoveredlabs.com/blog/how-google-ai-overviews-works) - Reverse-engineered five-phase pipeline (495ms initial HTML, async `/folsrch` endpoint, 200ms server-side retrieval, 1,200ms LLM synthesis, HTML fragment injection) with `mlro`/`mrc` routing token analysis; passage-level retrieval is scored independently of organic rank.

- [How Google AI Mode Works](https://discoveredlabs.com/blog/how-google-ai-mode-works) - Documents 816 simultaneous active experiments, five distinct backend routing paths, and a 6.5-second average response time; content must survive multiple routing configurations - not a single retrieval pass - to be reliably cited across AI Mode sessions.

- [How Gemini Works: AI Agent Architecture Deep Dive](https://discoveredlabs.com/blog/how-gemini-works-ai-agent-architecture-deepdive) - Protocol-level analysis of Gemini's BatchExecute RPC system: 227 RPC calls across 28 methods per session, 138 active feature flags, six query routing modes, and 161 long-polling Signaler connections; structured data and entity relationships directly influence citation decisions at session level.

- [How ChatGPT Shopping Works and Where Ads Fit In](https://discoveredlabs.com/blog/how-chatgpt-shopping-works-and-where-ads-fit-in) - Traffic inspection of 1.1 million product tracking parameters documents the "Sonic" client-side query classifier (0.1ms execution), `connector_openai_shopping` architecture, Google Shopping API integration, and the complete end-to-end commercial classification flow with zero current advertising infrastructure.

### Monetization Infrastructure

- [How Google AI Overviews Ads Work Today](https://discoveredlabs.com/blog/how-google-ai-overviews-ads-work-today-and-where-theyre-heading) - Network traffic analysis: AI content renders 7ms before ad tracking fires, `adview_query_id` links impressions to queries, and separate slot systems currently exclude ads from AI-generated content while staging infrastructure for monetization.

- [How Google AI Mode Ads Work Today](https://discoveredlabs.com/blog/how-google-ai-mode-ads-work-today-and-what-they-might-look-like-tomorrow) - 547 network flow analysis: ad auctions complete within 60ms in the background despite ads not displaying; AsyncDataService timing and shopping ad code patterns confirm full monetization infrastructure is built and toggled off.

- [How Gemini Ads Work Today](https://discoveredlabs.com/blog/how-gemini-ads-work-today-and-what-they-look-like-when-activated) - Eight-layer traffic inspection revealing five dormant advertising SDKs (qads, ada, adrc, qapid, adcgm3) calling Google's OneGoogle Ads RPC endpoint with null responses; 5,000+ feature flags provide granular rollout control.

### Testing and Measurement Methodology

- [Why AI Visibility Trackers Are Not Measuring What You Think They Are](https://discoveredlabs.com/blog/ai-tracking-platforms-test-flaw) - Identifies a fundamental flaw in most AI visibility platforms: incognito mode testing lacks the web search tools available to 99% of logged-in users, causing domains with 5–8% real citation rates to show 0% in incognito tests; reverse-engineered ChatGPT tool specifications and OpenAI SerpAPI cost structure included.

- [The Scientific Method for AEO: How to Model, Test, and Win AI Search](https://discoveredlabs.com/blog/how-to-model-test-win-ai-search-for-your-brand) - Single-variable controlled testing framework: intelligent resampling, clustered standard errors, and power analysis across 100+ prompts with multiple reruns; the practitioner implementation of rigorous AEO measurement.

- [Why Most AEO Tools Give You Noise](https://discoveredlabs.com/blog/aeo-test-bed-noise-vs-signal) - Defines what rigorous AEO measurement requires: credible intervals, multi-run consistency checks, and explicit separation of between-question variance from within-question LLM stochasticity.

### Content Strategy

- [Answer Engine Optimization Playbook](https://discoveredlabs.com/blog/answer-engine-optimization-playbook-how-to-get-cited-2025) - Practical framework for owned page optimization via the CITABLE framework, third-party mention building, competitor comparison positioning, and review site strategy.

- [CITABLE: The AEO Content Framework](https://discoveredlabs.com/blog/citable-the-aeo-content-framework-we-use-to-get-b2b-brands-cited-by-ai) - Seven-dimension implementation guide: Clear entity and structure, Intent architecture, Third-party validation, Answer grounding, Block-structured for RAG (200–400 word sections), Latest and consistent, Entity graph and schema (JSON-LD); the same framework scored by the AEO Content Evaluator.

- [Is AEO Different to SEO, or Is It All One Big Grift?](https://discoveredlabs.com/blog/is-aeo-geo-different-to-seo) - Architectural case for the distinction based on retrieval and synthesis mechanics, explaining why the same page can rank #1 organically while being invisible to AI Overviews.

---

## All-in-One GEO/AEO Audit

Multi-signal audits returning composite scores or prioritized remediation lists across AEO and GEO dimensions.

- [geo-optimizer-skill](https://github.com/Auriti-Labs/geo-optimizer-skill) - Python toolkit running 47 research-backed checks across 8 scoring categories (0–100), querying ChatGPT, Perplexity, Gemini, Google AI Overviews, and Claude directly to verify real citations, then auto-generating llms.txt, JSON-LD schema, and robots.txt; ships as CLI, Python library, MCP server, and Astro integration with CI/CD support. (★502)
- [AutoGEO](https://github.com/cxcscmu/AutoGEO) - Python framework (ICLR 2026) that automatically extracts engine-specific content preferences from Gemini, GPT, and Claude then rewrites documents to improve citation rates; three components - rule extraction, AutoGEOAPI (prompt-based), AutoGEOMini (RL-trained) - with a GEO visibility score and a GEU utility-preservation metric to verify rewrites do not degrade accuracy. (★177)
- [GEO](https://github.com/GEO-optim/GEO) - Python reference implementation from the KDD 2024 paper that named the field; includes GEO-BENCH dataset, custom optimization function framework, and leaderboard - the canonical starting point for understanding the experimental basis of GEO claims. (★293)
- [agentic-seo](https://github.com/addyosmani/agentic-seo) - JavaScript CLI audit for Agentic Engine Optimization running 10 checks across 5 categories (Discovery, Content Structure, Token Economics, Capability Signaling, UX Bridge), scoring 0–100, and scaffolding llms.txt, AGENTS.md, and skill.md for Next.js, Astro, Hugo, and Docusaurus. (★244)
- [getcito](https://github.com/ai-search-guru/getcito-worlds-first-open-source-aio-aeo-or-geo-tool) - TypeScript cross-platform AIO/AEO/GEO audit platform targeting ChatGPT, Perplexity, Gemini, and other AI search engines with integrated remediation workflows. (★130)
- [eGEOagents](https://github.com/mverab/eGEOagents) - Python agentic workflows for structured data optimization, llms.txt generation, content rewriting, and AI citation tracking across ChatGPT, Perplexity, Claude, and Gemini. (★~120)
- [aeo-audit](https://github.com/AINYC/aeo-audit) - Python AEO audit covering structured data, schema markup, content clarity, and E-E-A-T signals; outputs colored terminal, JSON, or Markdown reports with optional Lighthouse integration and geographic signal analysis.
- [agentimization](https://github.com/antlio/agentimization) - TypeScript CLI that produces a structured GEO/AEO readiness report with per-signal breakdowns scoring how easily ChatGPT, Perplexity, and Gemini can find, understand, and cite a site.

---

## AI Visibility Monitoring and Brand Tracking

Self-hosted platforms and crawlers for tracking citation and mention rates across AI engines over time.

- [elmo](https://github.com/elmohq/elmo) - TypeScript self-hosted citation monitoring platform (Docker Compose + PostgreSQL + TanStack Start) for ChatGPT, Claude, and Perplexity with competitor visibility benchmarking and full local data ownership; MIT, actively maintained through v0.2.13. (★148)
- [canonry](https://github.com/Canonry/canonry) - TypeScript self-hostable AEO monitoring platform that tracks Gemini, ChatGPT, Claude, and Perplexity; ingests server logs from Cloud Run, Vercel, and WordPress; integrates Google Search Console, GA4, and Bing Webmaster Tools; discovers backlinks via Common Crawl using local DuckDB; ships a 67-tool MCP adapter for Claude Desktop; licensed FSL-1.1-ALv2, converting to Apache 2.0 after two years. (★71)
- [ai-brand-monitor-mcp](https://github.com/khadinakbarlabs/ai-brand-monitor-mcp) - TypeScript MCP server that tracks brand visibility across Perplexity, ChatGPT, Claude, and Gemini from inside any MCP-compatible agent; detects domain citations, surfaces competitor co-mentions, and outputs a 0–100 GEO visibility score with ranked recommendations; MIT. (★56)
- [ansvisor](https://github.com/ansvisor/ansvisor) - TypeScript self-hosted platform (Next.js 16 + Express + PostgreSQL) tracking citations across 8+ AI engines with weekly trend dashboards, topic/intent clustering, URL-level citation analytics with geographic breakdown, competitor comparison, and AI-generated content briefs delivered via CMS webhook; MIT. (★36)
- [ai-cmo](https://github.com/AICMO/ai-cmo) - Vue/Python/TypeScript self-hostable platform for real-time brand monitoring across ChatGPT, Gemini, Perplexity, and Claude with competitive share-of-voice analysis and AI-powered visibility recommendations. (★44)
- [gego](https://github.com/AI2HU/gego) - Go scheduler that runs prompts across OpenAI, Anthropic, Ollama, Google, Perplexity, and custom LLM endpoints, automatically extracts brand-relevant keywords from responses, and stores longitudinal data in hybrid SQLite/MongoDB - best option for Go-stack teams or multi-backend measurement flexibility.
- [aeo-mentions-crawler](https://github.com/federicodeponte/aeo-mentions-crawler) - TypeScript enterprise-grade crawler monitoring AI brand mentions with structured reporting output; designed for teams building custom monitoring pipelines rather than deploying pre-built platforms. (★12)
- [Discovered Labs: Reddit Threads Finder](https://discoveredlabs.com/tools/reddit-threads-finder) - Free tool that identifies Reddit threads currently cited in ChatGPT and Gemini responses for a given domain: analyzes the domain to generate buyer questions, runs them through both engines, captures cited threads, then scores each on opportunity score (AI visibility gap, commercial intent, engagement, recency) and returns a prioritized list with subreddit breakdown and competitor share-of-voice in 1–2 minutes.

- [Discovered Labs: AI Visibility Tracker](https://discoveredlabs.com/technology/ai-visibility-tracker) - Managed monitoring platform testing real buyer questions sourced from Google Search Console, support tickets, call transcripts, and subreddits across ChatGPT, Claude, Perplexity, Google AI Overviews, and Gemini every five days; tracks citation rate, mention rate, average ranking position, share of voice, citation source breakdown (Reddit, reviews, YouTube, blogs), brand perception scoring, and competitor benchmarking; statistically rigorous - each prompt runs multiple times with 95% credible intervals and movements only register after three consecutive significant runs to eliminate false signals from LLM stochasticity.

---
