# Ten AIs Forecast the 2026 Senate

Ten AI models got the same dossier on the 13 most competitive U.S. Senate races of **November 3, 2026**: every public poll we could find since September 1, past election results, campaign money, key events and the national picture. Each model forecast every race in one request, with **no internet and no tools**, at its highest available setting.

Everything here is published **before any votes are counted**. After the election, every forecast is scored against the official results with rules that were fixed before the first model was run.

From the Novaki channel on YouTube ([@Novaki_ai](https://www.youtube.com/@Novaki_ai)). Video links are added here when they are published.

**Forecast video** (published Oct 31, 2026): https://youtu.be/k1n6dAKuJoA. The results video follows after the AP race calls.

## Timeline

| When (UTC) | What |
|---|---|
| Oct 31, 2026, 02:14 | Prompt, dossier and scoring rules locked ([`LOCK.sha256`](LOCK.sha256)). This is the first commit. |
| Oct 31, 2026, 02:20 | Rule change 1 logged in [`SCORING.md`](SCORING.md) during run 1 (Alaska and Maine use ranked-choice voting). The first lock is kept as `LOCK-v1.sha256`; `LOCK.sha256` is the current one. |
| Oct 31, 2026, 02:40 | All ten official forecasts (run 1) added to [`forecasts/`](forecasts/), with every raw reply, plus a snapshot of prediction markets and forecasting models taken at the time the models ran ([`snapshot-experts-and-markets-2026-10-31.json`](snapshot-experts-and-markets-2026-10-31.json)). Summary: [`forecasts/TABLE.md`](forecasts/TABLE.md). |
| Oct 31, 2026, 03:10 | Run 2 added for all ten models (the same request again in a fresh session, for consistency only; not used for the ranking). |
| After the AP race calls | Results and scores added. Races that are not called yet stay pending and are updated later. |

The commit history is the timestamp: GitHub records when each commit was pushed.

## The models

| Model | Company | Run through | Setting |
|---|---|---|---|
| Claude Fable 5.1 | Anthropic | Claude Code | high effort (its max setting is stopped by its own safeguards in Claude Code) |
| Claude Opus 5.5 | Anthropic | Claude Code | max effort |
| GPT-6 Astra | OpenAI | Codex | ultra reasoning |
| GPT-6.1 Sol | OpenAI | Codex | ultra reasoning |
| Gemini 4 Argon | Google | Antigravity | high |
| Gemini 3.8 Flash | Google | Antigravity | high |
| Grok 4.7 | xAI | Grok Build | xhigh effort |
| Kimi K3.1 Pro | Moonshot AI | Kimi Code | max effort |
| DeepSeek V4.1 Flash | DeepSeek | OpenCode (free tier) | max |
| GLM-5.3 Flash | Z.ai | OpenCode (free tier) | max |

Every model ran with clean settings: no personal instructions, memories, skills, plugins or connectors, and with web search and fetch turned off. Claude Code, Codex, Antigravity and Kimi Code ran with no tools at all (in Antigravity a hook blocks every tool call; none was attempted). Grok Build and OpenCode keep a read-only file tool, with nothing in their working folders. Grok Build shortened the long prompt in the message it sent, so in both runs Grok used that tool to read the rest of the same prompt from Grok Build's own saved copy (lines 838–1032) and opened nothing else. The two OpenCode models made no tool calls.

## The races

Alaska, Florida (special), Iowa, Kansas, Maine, Michigan, Minnesota, Nebraska, New Hampshire, North Carolina, Ohio (special), South Carolina and Texas: every 2026 Senate race that at least one of eleven published race raters (late October 2026) rated as toss-up, tilt or lean. The ratings themselves were **not** given to the models.

## Rules in short

- One prompt ([`prompt.md`](prompt.md)) and one dossier ([`dossier.md`](dossier.md)) for every model. The exact text each model received is `prompt.md` with `{{TARIH}}` replaced by "October 31, 2026" and `{{DOSYA}}` replaced by the contents of `dossier.md`.
- Deliberately left out of the dossier: expert race ratings, forecasting models, polling averages and betting odds. The models had to judge the raw evidence themselves.
- For each race a model names a winner, gives the probability that this candidate wins, and predicts both main candidates' vote shares. It also forecasts the number of Republican seats and the chance that Republicans keep control.
- Scoring ([`SCORING.md`](SCORING.md)): Brier score (main ranking), correct winners, margin error, partisan lean, Senate seat count and consistency between two identical runs. The same rules are applied to four baselines: polls only, prediction markets, forecasting models and a coin flip.
- Sources: [`data/`](data/) holds every race and the national file with a source link for each fact. Polls are as published by the pollsters (found through each race's Wikipedia polling table); money is from FEC filings.

## Verify the lock

```
sha256sum -c LOCK.sha256
```

## Note

This is a test of how well AI models forecast elections, not voting advice and not an endorsement of any candidate or party.

## License

Text, dossier and data compilation: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Poll results, filings and other source material belong to their publishers; links are in `data/`.
