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

## Technical AEO Infrastructure

Libraries, middleware, and configuration tools for serving AI-crawler-optimized content and implementing llms.txt, structured data, and robots.txt.

- [llms-txt-hub](https://github.com/thedaviddias/llms-txt-hub) - TypeScript/MDX searchable registry of production sites implementing the llms.txt standard, plus generators, validators, and integration guides for Next.js, Docusaurus, Hugo, and Astro - the authoritative resource for llms.txt tooling. (★863)
- [dualmark](https://github.com/dodopayments/dualmark) - TypeScript library that dual-serves clean Markdown to AI bots and polished HTML to humans from the same URL via HTTP content negotiation; six framework adapters (Next.js, Astro, SvelteKit, Cloudflare Workers, Deno Deploy, Vercel Edge); CLI conformance scorer (0–125 pts); automatic llms.txt generation and AI-vendor analytics hooks; Apache 2.0 with patent grant. (★91)
- [aeo.js](https://github.com/multivmlabs/aeo.js) - TypeScript framework-agnostic library generating llms.txt, robots.txt, sitemaps, and JSON-LD structured data; browser-based AI-crawler visibility scorer (0–100); widget for toggling AI-readable Markdown views; supports Astro, Next.js, Nuxt, Remix, SvelteKit, Angular, Vite, and plain CLI; MIT. (★100)
- [agent-seo](https://github.com/pontiggia/agent-seo) - TypeScript server middleware that auto-detects 17+ AI crawler user agents (GPTBot, ClaudeBot, and others) and serves clean Markdown instead of HTML; adapters for Next.js, Express, Fastify, and Hono - the server-side content negotiation layer for frameworks without a CDN transform step.
- [ai-seo-tools](https://github.com/RivalSee/ai-seo-tools) - Python template library of tools and prompts for llms.txt generation, robots.txt AI directives, structured data templates, and content formatting guidelines.

- [HTTP Headers as LLM Crawler Targets: 65,000 Pages Without HTML Parsing](https://metehan.ai/blog/http-headers-internal-links) - Technique encoding internal link graphs and heading hierarchies as base64url-compressed JSON in custom HTTP response headers (`X-Internal-Links`, `X-Headings`), delivering 8.6x faster crawl speeds via edge caching versus HTML parsing and exposing that 41.9% of pages were orphaned (unreachable via internal navigation); directly actionable for engineering teams adding LLM-crawler-specific metadata layers without modifying page HTML.
- [Discovered Labs: Agentic Browsing Checker](https://discoveredlabs.com/tools/agentic-browsing-checker) - Free tool that audits a public domain across 19 checks in the OPERABLE framework using Puppeteer, Lighthouse, and WebMCP W3C draft compliance testing: covers WebMCP tool registration, form annotation coverage, accessibility tree quality, tool schema JSON validity, llms.txt content validation, risky auto-submit detection, ARIA live region coverage, button keyboard operability, and AI crawler robots.txt access; delivers a scored report by email in 45–90 seconds.
- [webmachinelearning/webmcp](https://github.com/webmachinelearning/webmcp) - W3C Community Group Draft spec defining `navigator.modelContext.registerTool()` as a browser-native JS API for exposing web app tools to AI agents with zero server infrastructure; tools execute in page context sharing the user's existing auth session; authored by Microsoft and Google; security model covers tool poisoning, output injection, and cross-origin leakage. The foundational protocol reference for browser-side agent tool integration alongside server-side MCP.

- [Discovered Labs: AI Assist Widget](https://discoveredlabs.com/tools/ai-assist-widget) - Free tool: single script tag (<5KB minified, zero dependencies, CSS scoped with unique IDs) that adds floating buttons opening ChatGPT, Claude, Perplexity, Grok, or Gemini in a new tab with the current page URL pre-filled; configurable engine selection, position, colors, labels, and default prompt.

---

## Content Audit and Optimization

Tools that score, rewrite, or generate content to improve AI citation likelihood.

- [Discovered Labs: AEO Content Evaluator](https://discoveredlabs.com/tools/aeo-content-evaluator) - Free tool that scores pasted content up to 15,000 characters across seven CITABLE dimensions - Semantic Clarity (entity definitions, Q&A formatting, concept hierarchy), Citation & Answer Analysis (completeness, accuracy, expertise signals), RAG Optimization (structured elements, extractable facts), Third-party Validation (comparisons, credentials), Intent Architecture (query pathway coverage), Freshness & Consistency (temporal markers, cross-source alignment), and AI Detection (human vs. machine-generated assessment) - outputting an overall readiness score, strength/weakness breakdown, and prioritized improvement recommendations with re-evaluation capability.
- [Discovered Labs: Heading Optimizer](https://discoveredlabs.com/tools/heading-optimizer) - Free tool that generates 10+ headline variants, ranks them via pairwise tournament comparison using log probabilities to measure AI preference confidence, refines top candidates via beam search, and outputs a Pareto-optimal ranked list trading AI citation preference against Flesch-Kincaid readability; evaluates query fan-outs and AGREE citation grounding; most runs complete in 30–60 seconds.
- [seobuild-onpage](https://github.com/gbessoni/seobuild-onpage) - Python AI agent that generates complete pages by pulling the live SERP, analyzing top competitors, extracting People Also Ask data, finding content gaps, and writing structured pages with FAQ sections and schema markup; runs a 55-point post-generation quality checklist targeting both Google rankings and LLM citation via AI Overviews and Perplexity; bring-your-own-key for DataForSEO, GSC, Ahrefs, SEMRush; MIT. (★218)
- [google-ai-search-optimization](https://github.com/deepakness/google-ai-search-optimization) - Markdown agent skill operationalizing Google's published guidance for AI Overviews and AI Mode, covering structured data, E-E-A-T signals, passage indexing, and featured snippet optimization - useful as a workflow reference for content teams without a coding background. (★~128)

---

## SEO Research and Data Platforms

Crawlers, keyword tools, and data platforms that supply the underlying signals AEO decisions depend on.

- [open-seo](https://github.com/every-app/open-seo) - TypeScript open-source SEO platform providing keyword research, rank tracking, competitor analysis, backlink analysis, and site audits; exposes all functionality via an MCP interface for AI agent workflows; self-hostable via Docker or Cloudflare; powered by DataForSEO APIs with optional Google Search Console integration; MIT. (★3.1K)
- [firecrawl](https://github.com/firecrawl/firecrawl) - TypeScript library converting any URL to clean LLM-ready Markdown or structured data with dynamic page support, batch crawling, and site mapping - the de facto standard content extraction layer for competitive research, knowledge base construction, and SERP data pipelines. (★30K+)
- [gpt-researcher](https://github.com/assafelovic/gpt-researcher) - Python autonomous research agent that plans searches, scrapes, and synthesizes cited reports - the standard tool for building citation-worthy original research assets, the content format empirical AEO data shows dominates AI citations. (★27.9K)
- [seonaut](https://github.com/stjudewashere/seonaut) - Go SEO audit tool with an interactive Apache ECharts dashboard detecting broken links, redirect chains, missing or duplicate meta tags, and heading order issues; categorizes findings by critical/high/low severity; self-hostable via Docker. (★734)
- [python-for-seo](https://github.com/HasData/python-for-seo) - Python collection of seven specialized research tools: SERP Similarity Matrix, Content Gap Analyzer, AI Overview Monitor, Keyword Clustering via embeddings, rank tracking, and structured data validators.
- [seo-audits-toolkit](https://github.com/StanGirard/seo-audits-toolkit) - Python audit toolkit combining Lighthouse score audits, SERP rank tracking, keyword extraction, sitemap generation, header/link/image extraction, and security header checking; Docker support.

- [16 Months of GSC Data as a Vector Database](https://metehan.ai/blog/i-turned-16-months-of-google-search-console-data-into-a-vector-database-heres-what-i-learned) - Implementation guide: export GSC data, embed via Gemini, store in ChromaDB, query with natural language via Claude or Grok; demonstrates that vector search surfaces semantic query clusters SQL cannot find, while SQL remains necessary for exact metric filtering - establishes the hybrid SQL + vector DB pattern as the right measurement stack for AEO practitioners working from existing GSC data.
- [Mode VC WebMCP & Backlink Lens](https://modevc.com/tools/webmcp-backlink-lens) - Open-source Manifest V3 Chrome Extension and W3C WebMCP inspector for auditing dofollow/nofollow links and `.well-known/mcp.json` manifests.

---

## Agent Skill Packages

Pre-built skill sets for AI coding assistants (Claude Code, Cursor, Codex) exposing SEO and GEO capabilities as natural-language agent commands.

- [claude-seo](https://github.com/AgriciDaniel/claude-seo) - Python universal SEO skill for Claude Code with 25+ sub-skills and 18 specialist agents covering technical SEO, E-E-A-T, Schema.org (30+ types), GEO/AEO (/seo geo sub-skill), backlink analysis, local SEO, semantic clustering, and e-commerce; SPA-aware via Playwright; integrates Google Search Console, PageSpeed Insights, GA4, and optional DataForSEO/Firecrawl MCP extensions; MIT. (★9.9K)
- [seo-geo-claude-skills](https://github.com/aaron-he-zhu/seo-geo-claude-skills) - Python collection of 20 SEO and GEO skills compatible with Claude Code, Cursor, Codex, and 35+ AI agent platforms - broadest platform compatibility in this category. (★2.3K)
- [NotFair](https://github.com/nowork-studio/NotFair) - TypeScript Claude Code skills package covering SEO, GEO, Google Ads, and Meta Ads management via agent-native commands; for teams wanting cross-channel marketing coverage in a single package. (★3K)
- [codex-seo](https://github.com/AgriciDaniel/codex-seo) - Python Codex-first suite with 26 end-to-end workflows and 24 TOML agents covering technical audits, content optimization, reporting, and AEO/GEO checks; designed for autonomous operation in Codex and Claude Code environments. (★322)
- [recomby-geo](https://github.com/ViryaZheng/recomby-geo) - Python GEO-specific skill package combined with curated agent configuration lists; multi-platform support. (★522)
- [Agentic-SEO-Skill](https://github.com/Bhanunamikaze/Agentic-SEO-Skill) - Python skill suite with 16 specialized sub-skills, 10 specialist agents, and 88 optional utility scripts as evidence collectors producing structured SEO reports and action plans; compatible with Claude Code, Codex, Cursor, Windsurf, and Cline.

---

## Measurement and Calculators

Tools for statistically valid AEO measurement: sample size planning, variance accounting, and longitudinal engine tracking.

- [stanford-crfm/helm](https://github.com/stanford-crfm/helm) - Stanford CRFM's open evaluation framework covering 100+ scenarios and 50+ metrics with calibrated uncertainty; the statistical infrastructure for building rigorous AEO evaluation pipelines that produce confidence intervals rather than point estimates. Python, Apache 2.0.

- [DAIR.AI Prompt Engineering Guide](https://www.promptingguide.ai) - Elvis Saravia's comprehensive open guide covering prompting techniques, RAG architectures, chain-of-thought, and LLM evaluation; the practical reference for engineers building prompt-driven AEO optimization loops, automated scoring pipelines, and content rewriting workflows.

- [Discovered Labs: LLM Eval Calculator](https://discoveredlabs.com/tools/llm-eval-calculator) - Free tool that calculates statistically required sample sizes for measuring brand mention rates across AI platforms; uniquely accounts for both between-question variance (different prompts yield different mention rates, e.g. 60% vs. 20%) and within-question variance (LLM stochasticity across runs for the same prompt); users set confidence level (90/95/99%), margin of error (±0.5–5%), and resamples per prompt K (1–20); outputs unique prompts required, total API calls needed, and time estimates.
- [gego](https://github.com/AI2HU/gego) - Go scheduler that runs prompts across multiple LLM providers (OpenAI, Anthropic, Ollama, Google, Perplexity, custom endpoints) and stores longitudinal visibility results in hybrid SQLite/MongoDB - the open-source option for teams running their own multi-engine brand visibility studies over time.

---

## Related Lists

- [awesome-aeo-seo](https://github.com/discoveredlabs/awesome-aeo-seo) - Research papers, architecture references, and measurement methodology for AEO and GEO.
- [awesome-aeo-seo-agents](https://github.com/discoveredlabs/awesome-aeo-seo-agents) - Agent frameworks, MCP servers, and agentic workflow packages for AI search optimization.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, [Discovered Labs](https://discoveredlabs.com) has waived all copyright and related or neighboring rights to this work.
