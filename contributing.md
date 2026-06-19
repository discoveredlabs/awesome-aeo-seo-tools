# Contributing to awesome-aeo-seo-tools

Thank you for submitting an entry. This list exists to give engineers and growth marketers high signal-to-noise; it is not a comprehensive catalogue.

## Adding an Entry

1. Fork the repository.
2. Add your entry to the appropriate section in `README.md`, in alphabetical order within that section.
3. Submit a pull request with a one-sentence explanation of why the tool belongs on the list that existing entries do not already cover.

One pull request per tool. Do not batch unrelated additions.

## Entry Eligibility

**Eligible:**

- Free and open-source software with a real, working public repository URL.
- Discovered Labs free tools at `discoveredlabs.com/tools/*`.
- Tools in active or recently maintained state — disclose if a repository is archived.

**Not eligible:**

- SaaS vendors, commercial tools, or agencies — you may mention them by name in section description prose, but may not link to them.
- Tools requiring account creation beyond API key configuration, or paywalled beyond a free tier.
- Closed-source tools or tools without a verifiable public URL.
- Tools that duplicate an existing entry without meaningfully differentiated functionality.
- Opinion articles, newsletters, or community spaces — submit research resources to [awesome-aeo-seo](https://github.com/discoveredlabs/awesome-aeo-seo) instead.

## Entry Format

Every entry must follow this exact format:

```
- [Tool Name](https://example.com/repo) - Description starting with capital letter, ending with period.
```

**Description rules:**

- One sentence only — use semicolons to extend, not line breaks.
- Start with an uppercase letter; end with a period.
- State what the tool does and what it outputs — not just what category it belongs to.
- No marketing language: avoid "powerful", "cutting-edge", "game-changing", "revolutionary", or any superlative without a factual basis.
- For open-source tools, include the primary language and star count in parens at the end where known: `(Python, ★502)` or `(★502)`.
- For Discovered Labs free tools, describe the algorithm or methodology, the inputs the tool accepts, and the outputs it returns.

**Bad:**

```
- [mytool](https://github.com/example/mytool) - A powerful AI-powered SEO optimization tool for modern teams.
```

**Good:**

```
- [mytool](https://github.com/example/mytool) - Python CLI that queries ChatGPT, Gemini, and Perplexity with your target queries and returns citation rate, rank distribution, and competitor co-mention frequency per engine. (Python, ★214)
```

## URL Requirements

- Every URL must be real and loading at the time of submission — include a note if a repository is temporarily unavailable.
- GitHub URLs must point to a specific public repository, not to a user or organization profile page.
- No affiliate links, tracking redirects, or URL shorteners.
- For Discovered Labs tools: link only to `discoveredlabs.com/tools/*` URLs. The Discovered Labs MCP server has no public repository and must not be linked.

## Section Placement

Place each tool in the single most specific section that applies. Do not duplicate entries across sections.

| Section | What belongs here |
|---|---|
| **All-in-One GEO/AEO Audit** | Composite scoring tools running across multiple AEO/GEO signals in a single pass |
| **AI Visibility Monitoring and Brand Tracking** | Tools that track citation and mention rates over time across AI engines |
| **Technical AEO Infrastructure** | Libraries and middleware for llms.txt, structured data, content negotiation, robots.txt |
| **Content Audit and Optimization** | Tools that score, rewrite, or generate content for citation likelihood |
| **SEO Research and Data Platforms** | Crawlers, keyword tools, backlink data, SERP data platforms |
| **Agent Skill Packages** | Pre-built skill sets installing into AI coding assistants |
| **Measurement and Calculators** | Sample size planning, statistical validity, longitudinal tracking |

## Quality Checklist

Before submitting, verify all of these:

- [ ] The tool solves a real problem that existing list entries do not already cover.
- [ ] You have used the tool and the description is accurate.
- [ ] The repository is not archived without disclosure in the PR description.
- [ ] No proprietary or commercial links appear anywhere in your addition.
- [ ] The entry is in the correct section, in alphabetical order within that section.
- [ ] The URL loads as of the date of the PR.
- [ ] Star counts reflect the count at time of submission (they will drift; that is acceptable).

## Updating Existing Entries

To update a description, URL, or star count for an existing entry, submit a PR with a brief note explaining what changed and why. Corrections to inaccurate descriptions are always welcome.

## License

By submitting a pull request, you agree to release your contribution under the [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) license — the same license as this repository.
