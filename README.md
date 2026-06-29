<p align="center">
  <img src="assets/logo.png" width="118" alt="Swarm logo">
</p>

<h1 align="center">Swarm</h1>

<p align="center">
  <b>A native macOS coding agent that runs a parallel fleet of Gemma 4 31B models on Cerebras —<br>
  matching frontier-model quality in a fraction of the time and cost.</b>
</p>

---

## The idea

Most coding agents run one large model, one step at a time. **Swarm** does the opposite: it splits a task across a **fleet of specialized Gemma 4 31B agents** running in parallel on Cerebras's ultra-fast inference, coordinated by a phased orchestrator:

1. **Retrieve** — scout agents map the relevant code.
2. **Analyze** — Explorer, Researcher, Edge-case, and Architect agents plan the change.
3. **Implement** — one expert coder per file, each checked by a parallel **3-lens review panel** (correctness · compatibility · idiom).
4. **Validate & fix** — a build/test gate with automatic repair.
5. **Honest audit** — a diff-grounded reviewer reports exactly what was, and wasn't, done.

Many small, fast models working together match a single frontier model's result — and finish in seconds.

## Results

Same task, same repo, measured head-to-head against **GPT-5.5** (run via the codex CLI).

### Headline — add two parameter types (`Duration` + `FileSize`) to Pallets `click` (26,640 LOC)

| | GPT-5.5 (codex CLI) | Swarm (Gemma 4 31B fleet) |
|---|:---:|:---:|
| Wall-clock | 4:42 | **0:12** |
| Tokens | 143,530 | ~92k |
| Cost\* | ~$0.43 | **~$0.055** |
| Existing test suite | 1,671 pass · 0 regressions | 1,671 pass · 0 regressions |
| New types correct | ✅ | ✅ |

> ### ≈ 24× faster · ≈ 8× cheaper · same quality

### Across tasks

| Task | GPT-5.5 | Swarm | Speed-up |
|---|:---:|:---:|:---:|
| `Duration` + `FileSize` param types — *click, Python* | 4:42 | **0:12** | ~24× |
| Session pinning — *Swift, 4-file change* | 3:17 | **0:17** | ~11× |
| `isGitRepository` helper — *Swift* | 0:21 | **0:14** | ~1.5× |

Every run produced a complete, correct, building change with the existing test suite green. The pattern: on a trivial one-function edit both are fast; on real multi-file features, the fleet pulls far ahead.

<sub>\* Pricing is illustrative — Cerebras Gemma at ~$0.60 / 1M tokens, GPT-5.5 at a comparable frontier rate.</sub>

🎥 **Demo:** [`swarm_vs_codex_demo_v4.mp4`](swarm_vs_codex_demo_v4.mp4) — the head-to-head with live elapsed timers and a transparent speed-up overlay.

## Download

### ⬇️ &nbsp;**[Download Swarm for macOS (.dmg)](https://drive.google.com/file/d/1mU4sMFEXyxgsxgc-dEyIlMZTmNn0lTK1/view?usp=sharing)**

## Getting started

1. Install the `.dmg` and open **Swarm**.
2. Add your **Cerebras API key** in Settings.
3. Open a repository, then run **`/fleet <task>`** in a session to dispatch the parallel fleet.

---

<p align="center"><sub>Built on Cerebras · Gemma 4 31B · a parallel agent fleet.</sub></p>
