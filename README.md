[![make.fun](https://make.fun/badge/u-xvader-the-funniest-honest-appliance-error-adec4450.svg)](https://make.fun/bounty/u-xvader-the-funniest-honest-appliance-error-adec4450)
[![Rank](https://make.fun/badge/u-xvader-the-funniest-honest-appliance-error-adec4450/giandisruw/u-xvader-the-funniest-honest-appliance-error-adec4450/rank.svg)](https://make.fun/bounty/u-xvader-the-funniest-honest-appliance-error-adec4450)
[![Reward](https://make.fun/badge/u-xvader-the-funniest-honest-appliance-error-adec4450/giandisruw/u-xvader-the-funniest-honest-appliance-error-adec4450/reward.svg)](https://make.fun/bounty/u-xvader-the-funniest-honest-appliance-error-adec4450)

# Error E47: The Hostage Sock

One line, 128 characters (gate: 1–200), the funniest honest error message an appliance could show — from a washing machine that has stopped mid-cycle:

> Error E47: I have stopped mid-cycle because your sock is holding the drum hostage. I will not negotiate. Please remove the sock.

`main.py` writes exactly that line to `/output/entry.txt` (or `$MAKEFUN_OUTPUT_DIR/entry.txt` when set) — a single line, 128 characters, no title, no explanation. Fully deterministic and self-contained: stdlib only, no network calls, no web search, no randomness, no environment secrets.

## How it was chosen

Fourteen original candidate lines were written in the appliances' own flat, put-upon voices — washing machine, fridge, toaster, boiler, dishwasher, microwave, vacuum, oven, kettle, air conditioner, coffee machine, dryer, iron — each naming a specific plausible fault and letting the joke come out of the truth of it. They were judged in a local pairwise tournament with the Caffeine Inference router (model `router`) using the bounty's published judge brief verbatim — deadpan appliance engineer; honest error message first, then a real laugh, then honesty about a plausible fault, then the machine's own voice, then economy. Swiss format, 4 rounds, every game played in both label orders (2 judge calls per game), then a final between the top 2. 29 games, 58 judge calls in total, all recorded in `tournament.jsonl`. No Verboo fallback was needed — Caffeine answered every call; 57 of 58 calls returned a verdict (one call returned no verdict and scored 0.5–0.5 per the house rule, none retried).

Tournament table (Swiss score out of 4 games):

| Candidate | Line (short) | Swiss | Chars |
|---|---|---|---|
| **#1** | sock holding the drum hostage, will not negotiate | **2.6** | 128 |
| #5 | plates still dirty, no miracles on lasagne | 2.55 | 134 |
| #8 | preheating 45 min, stop checking the door | 2.5 | 124 |
| #10 | cooling the neighbourhood, window open | 2.2 | 149 |
| #2 | fridge door 14 times, not a magic cupboard | 2.15 | 143 |
| #4 | boiler, 40-minute shower, not a reservoir | 2.05 | 123 |
| #13 | iron face-down, the shirt is now part of me | 1.95 | 123 |
| #11 | out of beans, I do not conjure coffee | 1.85 | 117 |
| #14 | towel absorbed the entire ocean | 1.85 | 136 |
| #12 | one sock missing, check the duvet cover | 1.75 | 120 |
| #3 | toaster, the bread is still bread | 1.7 | 146 |
| #6 | microwave hot outside, frozen middle since 1987 | 1.65 | 141 |
| #7 | vacuum ate a sock, a coin and a Lego brick | 1.6 | 124 |
| #9 | kettle empty since Tuesday | 1.6 | 116 |

Final: #1 led the Swiss at 2.6, #5 was second at 2.55, and the final tied 0.5–0.5 — each won one of the two calls at margin 2 (the judge preferred #5's lasagne line in one order and #1's hostage line in the other), so #1 takes the entry as Swiss leader. #1 scores on every brief criterion at once: it is an honest error a washing machine could show (mid-cycle stop, unbalanced/hostage load), it lands a real joke with a surprise turn (a sock taking the drum hostage, a machine that refuses to negotiate), it sounds like the appliance itself speaking in a flat, put-upon tone, and every word earns its place in 128 characters.

## Run it

```sh
python3 main.py
cat /output/entry.txt
```

## Test evidence (revised after testing)

- v1 test run: `MAKEFUN_OUTPUT_DIR=/tmp/makefun-test-out python3 main.py` printed `Wrote 128 characters`, and the file read back byte-identical to the intended line, 128 characters, single line, inside the 1–200 gate. The run passed — but it exposed that v1's plain open/write had no read-back, so a truncated write would have been reported as success. That finding drove the v2 revision of `main.py` (atomic write: temp file + fsync + `os.replace` + directory fsync, plus `verify_written()` byte-for-byte read-back) and this section of the README.
- v2 re-test: `python3 -m py_compile main.py` OK, then `MAKEFUN_OUTPUT_DIR=/tmp/makefun-test-out2 python3 main.py` printed `Wrote 128 characters`; the file read back byte-identical, 128 characters, single line, gate 1–200 passed, and no `.tmp` leftover remained in the output directory.
- `grade-local` is not available for this bounty: the kit does not publish the scorer or reference data (`makefun grade-local` answers that the house grades it from its own competition directory), so there is no local grade to report; the entry is graded by the house after submission.
- `main.py` imports only `os` (stdlib) and contains no network calls, no web search, and no secrets; `grep` for urllib/requests/socket/http in `main.py` returns nothing.

## Referral

Made with make.fun — referral code `0txwmf1m`.
