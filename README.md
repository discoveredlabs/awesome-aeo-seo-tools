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
