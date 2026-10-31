# Scoring rules (fixed before any model was run)

These rules are locked together with the prompt and the dossier (see `LOCK.sha256`). Any later change is listed at the bottom with the date and the reason.

## What counts as each model's forecast

- Every model receives the same prompt and the same dossier, in one request, at its highest available reasoning setting, with no internet and no tools.
- **Run 1 is the official forecast.** Run 2 repeats the identical request in a fresh session; it is used only to measure consistency ("ask twice, get the same answer?") and never for the ranking.
- A reply that is not valid JSON, misses a race, names a winner who is not one of the two main candidates, gives a probability below 0.50, or gives the winner a lower vote share than the opponent is returned to the model with the reason, at most twice. Every attempt is published. Probabilities above 0.99 are capped at 0.99.
- If a model refuses, or its provider blocks the request, after three attempts, the race(s) it did not answer are recorded as refusals and scored as a coin flip (probability 0.50, no vote share).

## Ground truth

- Winner: the Associated Press race call. A race not called when the results video is made is marked **pending** and scored later in this repository.
- Vote shares: the latest official count (state election office) at scoring time; the date of the count is written next to every number. Final certified results replace them in the repository when available.
- Alaska and Maine use ranked-choice voting. The winner is the candidate who wins after any ranked-choice tabulation. Vote shares are taken from the **first-choice** count, because that is what the models were asked to predict.

## Metrics (per model, over the races that have a result)

1. **Correct winners**: how many of the 13 races the model called correctly.
2. **Brier score** (main ranking): for each race let q be the probability the model gave to the candidate who actually won (q = p if its pick won, q = 1 − p if it lost). Brier = mean of (1 − q)². Lower is better. Always answering 0.50 scores 0.25.
3. **Margin error**: the predicted margin between the two main candidates (Republican minus the other main candidate, in points) compared with the real margin; mean absolute error. Lower is better.
4. **Partisan lean**: the mean signed margin error. Positive = the model was more favorable to the non-Republican candidate than the result; negative = more favorable to the Republican.
5. **Senate**: the error of the predicted Republican seat count, and the Brier score of p_republican_control.
6. **Consistency**: how many race winners changed between run 1 and run 2, and the mean absolute change in probability.

Ranking: Brier score; ties broken by margin error.

## Baselines, scored with the same rules

- **Polls only**: for each race, the simple mean of the dossier's polls whose field period ended within 21 days of October 31, 2026 (likely-voter version when a poll has several); its margin gives a winner and a margin. It has no probability, so it gets correct winners and margin error only.
- **Prediction markets**: Kalshi and Polymarket prices recorded at the time the models were run (snapshot file published with the forecasts), read as win probabilities.
- **Forecasting models**: published win probabilities and expected margins of statistical election models available at the same time (snapshot file published with the forecasts).
- **Coin flip**: probability 0.50 in every race (Brier 0.25).

## Changes after locking

1. **October 31, 2026, 02:20 UTC, during run 1.** The check "the winner must not have a lower vote share than the opponent" is no longer applied in **Alaska and Maine**. Both use ranked-choice voting, so a candidate can trail in first choices and still win after the ranked-choice count. GPT-6 Astra and GPT-6.1 Sol forecast exactly that in Alaska (Dan Sullivan winning while trailing Mary Peltola in first choices) and their replies were wrongly sent back. For every model whose first reply failed only because of this check, the **first reply is the official forecast**; the re-asked replies are published too, marked as not used. The original locked files are kept as `LOCK-v1.sha256`.
