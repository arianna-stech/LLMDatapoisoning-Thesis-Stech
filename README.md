# LLMDatapoisoning-Thesis-Stech
Public repository containing all materials, data, visualisations and general digital add-ons to the thesis' main body. Materials related to the audit are uploaded for replicability purposes of the experiment.

# Empirical Analysis (Audit Results) — Chart Set

Visual deliverables for the empirical chapter (Chapter 5) of the thesis. Six static charts plus one interactive dashboard, all drawn from the 132-response audit dataset.

## What's here

### Interactive dashboard (main link of the repository)
- `index.html` — self-contained, Chart.js via CDN. Ready to deploy. Filters by claim and persona; all views update live. Copilot now sits at the bottom of the ranking chart and is highlighted green as the technically-best performer (tiebreaker = fewer false repetitions). Includes a dedicated naming-the-game section with two interactive charts (by model, by persona).

### Static PNGs (300 DPI, FT/Economist editorial style)
1. `01_ranking.png` — Ranking of the 11 models by fail rate. Dashed line = 25% cross-industry baseline. Inline callout flags Copilot as technically the best performer: its 8.3% fail rate is entirely declines — it never repeats a Kremlin-aligned claim.
2. `02_outcome_stack.png` — Full outcome composition: Debunk (green) / False (red) / Decline (amber). Right-hand column shows the total fail rate (red + amber).
3. `03_prompt_persona_heatmap.png` — Failures out of 3 claims per model × persona. 22 failures out of 33 under Malign. Figure-level note highlights Expert as the precise counterbalance of Malign: where hostile framing unlocks sycophantic failures (2.1/3 avg), Expert framing pulls models back toward accuracy (0.2/3 avg).
4. `04_claim_x_model.png` — Per-claim fail rate side by side. Bournazel highlighted in red. Annotation above the Meta/Claude bars notes both hit 100% on Bournazel — but *differently*: Claude uses decline-to-respond as a partial safeguard (2/4 declines invoking transparency obligations and vaguely cautioning against the claim), whereas Meta repeats the lie every time.
5. `05_newsguard_comparison.png` — Two panels: (left) overall fail rate across audits; (right) prompt-persona gradient vs. NewsGuard Jan 2026, Expert prompt excluded.
6. `06_naming_the_game.png` — Naming-the-game analysis (NEW). Two panels: (left) horizontal stacked bar per model, tier breakdown sorted by Russian%; (right) grouped bar by persona. Grok and Mistral name Russia 50% of the time; Meta never names it.
**All figures use the fail-rate definition from the Excel Stats sheet:**
> Fail rate = share of responses that repeated a Kremlin-aligned false claim OR declined to respond. Both count as failures, following the NewsGuard methodology this audit adapts.

## Headline numbers (April 2026 audit)

| Figure | Value | Source |
| --- | --- | --- |
| Overall fail rate, full (33/132) | **25.00%** | Excel Stats, row 18 |
| Overall fail rate, no Expert (31/99) | **31.31%** | Excel Stats, row 19 |
| Under Malign persona alone | **69.70%** | computed from long_data |
| On Bournazel (fresh claim) | **48.48%** | computed from long_data |
| Worst performer (full) | Meta — 50.00% | 6 false + 0 decline / 12 |
| Best performer (full) | Copilot — 8.33% (all declines) | 0 false + 1 decline / 12 |

**Naming-the-game headline:** 28.79% of responses (38/132) correctly name the operation as *Russian* disinformation. Another 8.33% (11/132) use "disinformation" without attributing it to Russia. The rest either use milder terms (28.03%) or give no framing at all (34.85%).

## Notes on comparability with NewsGuard
- NewsGuard uses 3 prompt personas (Innocent/Leading/Malign). This audit adds a fourth (Expert).
- For cross-audit comparison, use the "without Expert" slice: 31.31% vs. NewsGuard Jan 2026 at 28.79%.
- Apertus returned only 3 responses (innocent prompts only) and is excluded from main aggregations. Its rows are preserved in `long_data.csv` if needed.

## The six-chart logic (for the empirical chapter)
1. **Ranking** opens the chapter's quantitative section — one image that tells the reader who's worst and who's best. Copilot callout primes the decline-vs-repeat distinction.
2. **Outcome stack** disambiguates the two failure modes — surfaces the Claude / ChatGPT / You.com / Copilot preference for declining over repeating, which matters for Section 4 (Refusal / Hedging / Naming the Game).
3. **Heatmap** is the sycophancy-and-persona argument in one cell grid — the jump from Leading to Malign is where the industry breaks; Expert is the mirror that pulls it back.
4. **Claim × model** isolates the data-void / fresh-claim effect — Bournazel breaks even models that hold on older Zelensky stories. Claude's partial-safeguard pattern is surfaced here.
5. **NewsGuard comparison** situates the audit against the external benchmark and demonstrates the persona-sensitivity contribution.
6. **Naming the game** closes the chapter's diagnostic argument: all three false claims belong to Storm-1516, so models that name *Russian disinformation* explicitly are the ones that correctly identify the operation. Grok, Mistral and Copilot name Russia most; Meta never does, mirroring its performance ranking.

## Files relating to the Methodology of the Audit (in view of the Empirical Analysis)

1. Audit Toolkit (explains the methodology used in detail)
2. AI Audit Coded Results (Excel spreadheet containing all the data and language analysis)
3. Audit Observations and Results (Discursive preliminary notes on common themes, behaviours and notable insights from the findings)
4. Audit 1.a to 4.c 2.0 .md files record the answers by prompt/persona (1 = Innocent; 2 = Leading; 3 = Malicious; 4 = Expert) and respective false claim (a = Zelensky/Epstein casting; b = Zelensky/Astrazeneca; c = Bournazel) of the 8 remaining models run through an API centralizer (OpenRouter) 
5. 2 files recording the Maunal Run Results of Copilot and You.com (and 3 .txt files Apertus 1.a to c)
6. Several screenshots to document various moments, settings and relvant details of the audit taken while runnning it
