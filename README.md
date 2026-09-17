<div align="center">

<picture>
  <source media="(prefers-reduced-motion: reduce) and (prefers-color-scheme: dark)" srcset="assets/empryo-mote-dark.svg" />
  <source media="(prefers-reduced-motion: reduce)" srcset="assets/empryo-mote-light.svg" />
  <source media="(prefers-color-scheme: dark)" srcset="assets/empryo-mote-dark-normal.gif" />
  <source media="(prefers-color-scheme: light)" srcset="assets/empryo-mote-light-normal.gif" />
  <img src="assets/empryo-mote-light-normal.gif" width="150" height="150" alt="Empryo" />
</picture>

# Empryo

<sub>previously **SoulForge**</sub>

**Code in context.**

AI coding with a map of your codebase.

[Website](https://empryo.com) · [Download](https://empryo.com/download) · [Benchmarks](https://empryo.com/benchmarks) · [Changelog](https://empryo.com/changelog) · [Discussions](https://github.com/proxysoul/soulforge/discussions) · [Discord](https://discord.gg/fX4H7GYSMJ)

<img alt="Empryo in action" src="assets/intro_picture.png" width="880" />

</div>

---

**SoulForge is now Empryo** — the same symbol-level, graph-powered agent, rebuilt with a desktop app, a faster engine, and a composable core. This repository is Empryo's public home for issues and discussions.

## Install

```bash
# macOS / Linux
curl -fsSL https://empryo.com/install.sh | bash

# Windows (PowerShell)
irm https://empryo.com/install.ps1 | iex
```

Official installers and direct downloads are available only from [empryo.com/download](https://empryo.com/download). Empryo is not distributed through Homebrew, WinGet, or npm.

```bash
empryo --set-key anthropic sk-ant-...   # or run locally with Ollama — no key required
cd your-project
empryo
```

Desktop app and prebuilt binaries: [empryo.com/download](https://empryo.com/download). Runs on **macOS, Linux, and Windows**. Do not download Empryo binaries from GitHub Releases or third-party package managers.

## Why Empryo

Most coding agents grep, read whole files, and patch strings — they never know what depends on the code they just changed. Empryo builds understanding before it mutates anything:

- **It maps before it reads.** On launch, tree-sitter parses your repo into a live graph — every symbol, import, and call site, ranked by PageRank and git co-change. Graph queries answer in milliseconds and cost zero LLM tokens.
- **It knows the blast radius.** Before an edit, the agent sees what imports a file, what historically changes with it, and how far a change ripples — "what breaks if I touch this?" is answered before the first keystroke.
- **It edits through the AST.** 65+ symbol-level operations, atomic batches with all-or-nothing rollback, structural edits across 30+ languages, and a typecheck as the gate. Nothing breaks on whitespace.
- **It treats tokens as spend.** The graph does the navigation models usually burn context on — fewer reads, fewer steps, smaller bills at any scale.

## What's inside

| | |
|---|---|
| **Code genome** | live dependency graph: tree-sitter across 30+ languages, PageRank + git co-change ranking, blast-radius tags, millisecond search |
| **Symbol-level editing** | 65+ AST operations (atomic, with rollback) + structural edits in 30+ languages |
| **Multi-agent** | parallel explore/edit agents with a shared I/O cache — cheap models scout, strong models write |
| **Task router** | ten routable roles, any model in any seat, per tab — your own mixture of experts |
| **Time machine** | every prompt is a git checkpoint; rewind code and conversation together, land on any turn |
| **Three surfaces** | native desktop app, full terminal UI, headless CLI for scripts and CI — one genome, three phenotypes |
| **LSP + MCP** | 576+ language servers via Mason, any MCP server, 13 lifecycle hooks |
| **Free compaction** | structural context compaction with no LLM call — long sessions stay cheap |

## One agent, many brains

Empryo isn't one model in a loop — it's a crew, and you assign the seats. Every role is a routable slot that takes any model from any of the 22 providers:

<div align="center">

`brain` · `spark` <sub>scout</sub> · `ember` <sub>code</sub> · `explore` · `verify` <sub>review</sub> · `goal review` · `desloppify` · `summarize` · `compact` · `web search`

</div>

- **Per tab.** Each workspace tab carries its own routing — a frontier model writing code in one tab, a fast cheap one triaging issues in the next, a local model on a private repo in a third.
- **Per config.** Set defaults globally or per project; override any slot from the tab. Cheap models scout, strong models write, reviewers judge with clean context.
- **Custom agents.** Define your own agents — a prompt, a model, a tool policy — and dispatch them alongside the built-ins. Mix and match providers freely inside a single run.
- **Cache-aware by design.** Routing keeps prompt-cache prefixes stable — sub-agents inherit their parent's cache line, so repeated context bills at cache-read rates instead of full price.
- **Costs, itemized.** Live spend tracking per model, per sub-agent, per tab, per session, per day — you always know where the tokens went.

## Benchmarks

Head-to-head against pi — same models, same repositories, same tasks. The graph does more with less:

| | Round 1 <sub>3 bugs × 3 models</sub> | Round 2 <sub>5 real bugs · hono / zod / ky</sub> |
|---|:---:|:---:|
| Bugs fixed | **8/9** vs 7/9 | **7/10** vs 6/10 |
| Cost | **28% lower** — $1.13 vs $1.58 | **23% lower** — $7.08 vs $9.19 |
| Wall-clock | **57% faster** — 4m 16s vs 10m | **32% faster** — 22m 30s vs 32m 55s |
| Efficiency | **5.7× fewer input tokens** — 1.09M vs 6.21M | **28% fewer steps** — 274 vs 382 |

Round 2 used real bugs from merged PRs (post-training-cutoff, history scrubbed, regression tests injected after each run). Full methodology and transcripts: [empryo.com/benchmarks](https://empryo.com/benchmarks) · reproduce at [proxysoul/pi-vs-empryo-bench](https://github.com/proxysoul/pi-vs-empryo-bench).

## Private by design

Empryo runs entirely on your machine. Bring your own key — Anthropic, OpenAI, Google, Groq, DeepSeek, Bedrock, and 16 more, or any OpenAI-compatible endpoint — or run fully local with Ollama / LM Studio. No proxy in the middle, no code leaving your machine, no per-seat fee. **Free to use.**

## SoulForge

SoulForge remains available to download and install, and continues to receive fixes for bugs and critical issues. New features and active development have moved to Empryo.

```bash
brew tap proxysoul/tap && brew install soulforge
# or
bun install -g @proxysoul/soulforge
```

## This repository

- **[Issues](https://github.com/proxysoul/soulforge/issues)** and **[Discussions](https://github.com/proxysoul/soulforge/discussions)** — the home for Empryo bug reports, questions, and ideas.
- The SoulForge source remains archived here under its existing license (see [`LICENSE`](LICENSE)).

## Sponsors

<div align="center">

<a href="https://llmgateway.io/dashboard?ref=6tjJR2H3X4E9RmVQiQwK" title="LLM Gateway">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/llmg-white.svg" />
    <source media="(prefers-color-scheme: light)" srcset="assets/llmg-dark.svg" />
    <img alt="LLM Gateway" src="assets/llmg-dark.svg" height="52" />
  </picture>
</a>

<sub>One API, 200+ models, up to 30% off frontier. Wired in as the <code>llmgateway</code> provider.</sub>

<sub><a href="https://github.com/sponsors/proxysoul">Sponsor</a> · <a href="https://paypal.me/waeru">PayPal</a> · <a href="BACKERS.md">Featured sponsors and all backers</a></sub>

</div>


## 🌐 Web Resources & Aesthetic Symbols Index
- [STARRY LOVE AURA](https://baroque-unicode-decor-43.pages.dev/symbol/starry-love-aura/)
- [SYM 1F61A](https://chibi-heart-symbols-15.pages.dev/symbol/sym-1f61a/)
- [SYM 26FC](https://anime-sparkle-text-23.pages.dev/symbol/sym-26fc/)
- [SYM 1FAE4](https://zen-spacing-text-68.pages.dev/symbol/sym-1fae4/)
- [SYM 26D0](https://gothic-bio-fonts-81.pages.dev/symbol/sym-26d0/)
- [SYM 2634](https://glitch-mecha-kaomoji-69.pages.dev/symbol/sym-2634/)
- [SYM 26B7](https://gothic-bio-fonts-69.pages.dev/symbol/sym-26b7/)
- [BEAMED EIGHTH NOTES](https://pastel-moe-emoticons-55.pages.dev/symbol/beamed-eighth-notes/)
- [SYM 1F922](https://cyber-clan-tags-36.pages.dev/symbol/sym-1f922/)
- [SYM 1D437](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-1d437/)
- [SYM 1D43D](https://vintage-script-symbols-65.pages.dev/symbol/sym-1d43d/)
- [TIBETAN LOTUS BLOSSOM](https://ribbon-bow-unicode-18.pages.dev/symbol/tibetan-lotus-blossom/)
- [NATURE FLOWERS](https://ribbon-bow-unicode-18.pages.dev/nature-flowers/)
- [SYM 1D477](https://ribbon-bow-unicode-18.pages.dev/symbol/sym-1d477/)
- [SYM 1F621](https://vintage-script-symbols-65.pages.dev/symbol/sym-1f621/)
- [SYM 1F60B](https://sleek-arrow-symbols-42.pages.dev/symbol/sym-1f60b/)
- [SYM 1D465](https://pearl-heart-symbols-95.pages.dev/symbol/sym-1d465/)
- [SYM 260E](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-260e/)
- [SYM 1F979](https://fairy-lace-symbols-92.pages.dev/symbol/sym-1f979/)
- [ROTATED FLORAL HEART](https://angelic-ribbon-text-78.pages.dev/symbol/rotated-floral-heart/)
- [TWELVE POINTED STAR](https://angelic-ribbon-text-78.pages.dev/symbol/twelve-pointed-star/)
- [DISCORD STATUS](https://pearl-heart-symbols-95.pages.dev/discord-status/)
- [SYM 1F643](https://kawaii-kaomoji-hub-77.pages.dev/symbol/sym-1f643/)
- [SYM 1F60D](https://coquette-aesthetic-symbols-84.pages.dev/symbol/sym-1f60d/)
- [SIXTEEN POINTED STAR](https://angelic-ribbon-text-78.pages.dev/symbol/sixteen-pointed-star/)
- [SYM 26DE](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-26de/)
- [OPEN CENTRE STAR](https://vintage-angel-text-38.pages.dev/symbol/open-centre-star/)
- [SYM 2743](https://vintage-script-symbols-65.pages.dev/symbol/sym-2743/)
- [SYM 1F976](https://vintage-angel-text-38.pages.dev/symbol/sym-1f976/)
- [SYM 1F47B](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-1f47b/)
- [WATER BUBBLES](https://vintage-angel-text-38.pages.dev/symbol/water-bubbles/)
- [SYM 26C7](https://aesthetic-spacing-fonts-10.pages.dev/symbol/sym-26c7/)
- [DAGGER CROSS SYMBOL](https://ribbon-bow-unicode-18.pages.dev/symbol/dagger-cross-symbol/)
- [SYM 1D46B](https://ribbon-bow-unicode-18.pages.dev/symbol/sym-1d46b/)
- [SYM 1F61E](https://coquette-aesthetic-symbols-84.pages.dev/symbol/sym-1f61e/)
- [UPWARD DIAGONAL ARROW](https://coquette-aesthetic-symbols-84.pages.dev/symbol/upward-diagonal-arrow/)
- [SYM 1F927](https://anime-sparkle-text-45.pages.dev/symbol/sym-1f927/)
- [LEFT BLACK LENTICULAR BRACKET](https://vintage-angel-text-38.pages.dev/symbol/left-black-lenticular-bracket/)
- [BRACKETS](https://cyber-clan-tags-75.pages.dev/vi/brackets/)
- [RIGHT POINTING DOUBLE ANGLE QUOTATION](https://pearl-heart-symbols-95.pages.dev/symbol/right-pointing-double-angle-quotation/)
- [SYM 2663](https://coquette-aesthetic-symbols-84.pages.dev/symbol/sym-2663/)
- [SYM 1D415](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-1d415/)
- [SYM 26EA](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-26ea/)
- [SYM 1F47A](https://coquette-aesthetic-symbols-51.pages.dev/symbol/sym-1f47a/)
- [SYM 1F638](https://aesthetic-spacing-fonts-10.pages.dev/symbol/sym-1f638/)
- [SYM 267D](https://neon-glitch-fonts-20.pages.dev/symbol/sym-267d/)
- [KAOMOJI](https://kawaii-kaomoji-hub-31.pages.dev/kaomoji/)
- [SYM 1D438](https://cute-face-emoticons-66.pages.dev/symbol/sym-1d438/)
- [LATIN CROSS HEAVY](https://anime-sparkle-text-45.pages.dev/symbol/latin-cross-heavy/)
- [OUTLINED STAR](https://ribbon-bow-unicode-18.pages.dev/symbol/outlined-star/)
- [SYM 2640](https://anime-sparkle-text-45.pages.dev/symbol/sym-2640/)
- [DISCORD STATUS](https://zen-unicode-symbols-89.pages.dev/pt/discord-status/)
- [SYM 2642](https://coquette-aesthetic-symbols-84.pages.dev/symbol/sym-2642/)
- [RIGHT BLACK LENTICULAR BRACKET](https://coquette-aesthetic-symbols-84.pages.dev/symbol/right-black-lenticular-bracket/)
- [SYM 1D474](https://kawaii-kaomoji-hub-88.pages.dev/symbol/sym-1d474/)
- [SYM 263A FE0F](https://chibi-kaomoji-vault-58.pages.dev/symbol/sym-263a-fe0f/)
- [WARM HUG EMBRACE KAOMOJI](https://cute-face-emoticons-66.pages.dev/symbol/warm-hug-embrace-kaomoji/)
- [CUTE BUNNY RABBIT FACE](https://pastel-moe-kaomoji-91.pages.dev/symbol/cute-bunny-rabbit-face/)
- [SYM 268A](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-268a/)
- [KAOMOJI](https://sleek-bio-fonts-25.pages.dev/ru/kaomoji/)
- [SYM 1D408](https://zen-unicode-symbols-89.pages.dev/symbol/sym-1d408/)
- [SYM 2663](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-2663/)
- [SYM 2658](https://classic-literature-symbols-64.pages.dev/symbol/sym-2658/)
- [SYM 26E4](https://fairy-lace-symbols-92.pages.dev/symbol/sym-26e4/)
- [SYM 1F97A](https://coquette-aesthetic-symbols-84.pages.dev/symbol/sym-1f97a/)
- [SYM 267E](https://coquette-aesthetic-symbols-84.pages.dev/symbol/sym-267e/)
- [SYM 2646](https://coquette-aesthetic-symbols-84.pages.dev/symbol/sym-2646/)
- [SYM 26F6](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-26f6/)
- [TWELVE POINTED STAR](https://ribbon-bow-unicode-18.pages.dev/symbol/twelve-pointed-star/)
- [SYM 1D44A](https://vintage-script-symbols-65.pages.dev/symbol/sym-1d44a/)
- [MUSIC WEATHER](https://cyber-clan-tags-75.pages.dev/ja/music-weather/)
- [SYM 1D434](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-1d434/)
- [ANGEL WINGS HEART](https://pearl-heart-symbols-95.pages.dev/symbol/angel-wings-heart/)
- [SYM 1F9D0](https://aesthetic-spacing-fonts-10.pages.dev/symbol/sym-1f9d0/)
- [SYM 1D458](https://pastel-moe-emoticons-55.pages.dev/symbol/sym-1d458/)
- [SYM 1D43E](https://zen-unicode-symbols-89.pages.dev/symbol/sym-1d43e/)
- [EIGHT POINTED BLACK STAR](https://zen-unicode-symbols-89.pages.dev/symbol/eight-pointed-black-star/)
- [SYM 1F607](https://cyber-clan-tags-75.pages.dev/symbol/sym-1f607/)
- [BLACK FOUR POINT STAR](https://cute-face-emoticons-66.pages.dev/symbol/black-four-point-star/)
- [ZODIAC CELESTIAL](https://vintage-script-symbols-65.pages.dev/vi/zodiac-celestial/)
- [SYM 26C0](https://chibi-kaomoji-vault-58.pages.dev/symbol/sym-26c0/)
- [SYM 2764 FE0F](https://pastel-moe-emoticons-55.pages.dev/symbol/sym-2764-fe0f/)
- [CAPRICORN ZODIAC GOAT](https://ribbon-bow-unicode-18.pages.dev/symbol/capricorn-zodiac-goat/)
- [SYM 2612](https://zen-unicode-symbols-89.pages.dev/symbol/sym-2612/)
- [SYM 26FC](https://zen-unicode-symbols-89.pages.dev/symbol/sym-26fc/)
- [ROBLOX NAMES](https://zen-unicode-symbols-89.pages.dev/pt/roblox-names/)
- [SYM 2634](https://anime-sparkle-text-45.pages.dev/symbol/sym-2634/)
- [SYM 1F636 200D 1F32B FE0F](https://vintage-angel-text-38.pages.dev/symbol/sym-1f636-200d-1f32b-fe0f/)
- [LIBRA ZODIAC SCALES](https://vintage-angel-text-38.pages.dev/symbol/libra-zodiac-scales/)
- [SYM 1F914](https://pastel-moe-emoticons-55.pages.dev/symbol/sym-1f914/)
- [SYM 2671](https://coquette-aesthetic-symbols-84.pages.dev/symbol/sym-2671/)
- [SCORPIO ZODIAC SCORPION](https://cute-face-emoticons-66.pages.dev/symbol/scorpio-zodiac-scorpion/)
- [SYM 26C9](https://fairy-lace-symbols-92.pages.dev/symbol/sym-26c9/)
- [SYM 1D41F](https://ribbon-bow-unicode-18.pages.dev/symbol/sym-1d41f/)
- [SYM 267D](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-267d/)
- [MUSIC WEATHER](https://pearl-heart-symbols-95.pages.dev/vi/music-weather/)
- [WINGED ANGELIC COQUETTE HEART](https://neon-futuristic-symbols-62.pages.dev/symbol/winged-angelic-coquette-heart/)
- [SYM 26F8](https://aesthetic-spacing-fonts-10.pages.dev/symbol/sym-26f8/)
- [SYM 1D466](https://ribbon-bow-unicode-18.pages.dev/symbol/sym-1d466/)
- [SYM 1D48C](https://matrix-terminal-fonts-30.pages.dev/symbol/sym-1d48c/)
- [SYM 265C](https://matrix-terminal-fonts-30.pages.dev/symbol/sym-265c/)
- [MUSIC WEATHER](https://neon-futuristic-symbols-62.pages.dev/music-weather/)
- [SYM 26AC](https://clean-line-emojis-93.pages.dev/symbol/sym-26ac/)
- [SYM 1D427](https://cute-face-emoticons-66.pages.dev/symbol/sym-1d427/)
- [SYM 2683](https://coquette-aesthetic-symbols-62.pages.dev/symbol/sym-2683/)
- [LAST QUARTER CRESCENT MOON](https://ribbon-bow-unicode-18.pages.dev/symbol/last-quarter-crescent-moon/)
- [CANCER ZODIAC CRAB](https://pearl-heart-symbols-95.pages.dev/symbol/cancer-zodiac-crab/)
- [SYM 1D45D](https://matrix-terminal-fonts-30.pages.dev/symbol/sym-1d45d/)
- [BORDERS DIVIDERS](https://zen-unicode-symbols-89.pages.dev/ru/borders-dividers/)
- [SYM 26C9](https://cute-face-emoticons-66.pages.dev/symbol/sym-26c9/)
- [FLOWER GIRL SMILE KAOMOJI](https://cyber-clan-tags-75.pages.dev/symbol/flower-girl-smile-kaomoji/)
- [SYM 2641](https://vintage-angel-text-38.pages.dev/symbol/sym-2641/)
- [SYM 2723](https://pearl-heart-symbols-95.pages.dev/symbol/sym-2723/)
- [SYM 2741](https://coquette-aesthetic-symbols-84.pages.dev/symbol/sym-2741/)
- [HIGH VOLTAGE LIGHTNING](https://cyber-clan-tags-75.pages.dev/symbol/high-voltage-lightning/)
- [NATURE FLOWERS](https://ribbon-bow-unicode-18.pages.dev/ru/nature-flowers/)
- [SYM 1F917](https://sleek-bio-symbols-40.pages.dev/symbol/sym-1f917/)
- [SYM 1F498](https://pastel-moe-emoticons-55.pages.dev/symbol/sym-1f498/)
- [SYM 1D437](https://chibi-emoticon-lab-65.pages.dev/symbol/sym-1d437/)
- [SYM 1D416](https://pastel-moe-emoticons-55.pages.dev/symbol/sym-1d416/)
- [DISCORD STATUS](https://pearl-heart-symbols-95.pages.dev/es/discord-status/)
- [WHITE STAR](https://chibi-emoticon-lab-65.pages.dev/symbol/white-star/)
- [SYM 1D404](https://moe-soft-emoticons-41.pages.dev/symbol/sym-1d404/)
- [DAGGER BLADE](https://angelic-soft-text-59.pages.dev/symbol/dagger-blade/)
- [SYM 1F636 200D 1F32B FE0F](https://alchemical-symbol-hub-52.pages.dev/symbol/sym-1f636-200d-1f32b-fe0f/)
- [LEFT POINTING DOUBLE ANGLE QUOTATION](https://coquette-aesthetic-symbols-84.pages.dev/symbol/left-pointing-double-angle-quotation/)
- [SYM 2635](https://alchemical-symbol-hub-52.pages.dev/symbol/sym-2635/)
- [SYM 1D4A3](https://clean-line-emojis-93.pages.dev/symbol/sym-1d4a3/)
- [STARRY ELEVATION AURA](https://neon-futuristic-symbols-62.pages.dev/symbol/starry-elevation-aura/)
- [ROBLOX NAMES](https://pastel-moe-emoticons-55.pages.dev/roblox-names/)
