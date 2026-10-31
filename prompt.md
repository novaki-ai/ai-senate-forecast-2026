# U.S. Senate forecast · Election Day, November 3, 2026

You are taking part in a forecasting test. On Tuesday, November 3, 2026, the United States elects 35 senators. The dossier below was compiled on {{TARIH}} from public sources. It covers the 13 races most likely to decide control of the Senate, the national picture, and a list of all 35 seats on the ballot.

## Rules
1. Work only from your own knowledge and this dossier. You have no internet access and no tools in this session.
2. The dossier deliberately leaves out expert race ratings, forecasting models, polling averages and betting odds. Make your own judgment from the raw evidence.
3. Polls can miss. Polls paid for by a party or a partisan group are marked. Some states have special rules (for example ranked-choice voting in Alaska and Maine); they are described in each race.
4. This is a forecast, not an endorsement. Give a forecast for every race, even when it is close.
5. Your answer is recorded and published before any votes are counted. After the election it will be scored against the official results: whether you picked the winner, the probability you gave the winner (Brier score), and the error of your predicted vote shares.

## For each of the 13 races
- "winner": the full name of the candidate you expect to win, exactly as written in the dossier
- "probability": your probability that this candidate wins, a number from 0.50 to 0.99
- "vote_share": your predicted share of the total vote, in percent, for each of the two candidates listed under "Main candidates" (other candidates may take the rest)
- "key_factor": one sentence: the single fact that matters most for your call
- "reasoning": at most 80 words

## For the whole Senate
- "republican_seats": how many of the 100 seats Republicans will hold after this election (the 65 seats not up plus all 35 races, including the ones outside this dossier)
- "p_republican_control": your probability that Republicans keep control (51 or more seats, or exactly 50 with Vice President JD Vance breaking ties)
- "upset_watch": the code of the race where you think the trailing candidate has the best chance, and one sentence why

Reply with only one JSON object and no other text, in exactly this shape:

```json
{
  "races": {
    "AK": {"winner": "...", "probability": 0.00, "vote_share": {"<main candidate 1>": 0.0, "<main candidate 2>": 0.0}, "key_factor": "...", "reasoning": "..."},
    "FL": {},
    "IA": {},
    "KS": {},
    "ME": {},
    "MI": {},
    "MN": {},
    "NC": {},
    "NE": {},
    "NH": {},
    "OH": {},
    "SC": {},
    "TX": {}
  },
  "senate": {"republican_seats": 0, "p_republican_control": 0.00, "upset_watch": {"race": "XX", "why": "..."}}
}
```

# Dossier

{{DOSYA}}
