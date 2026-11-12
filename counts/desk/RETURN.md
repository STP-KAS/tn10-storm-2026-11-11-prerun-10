MET

Scored on submit-OK, not on inclusion. Inclusion, reported and not scored: in 3 of 3 minutes our payments included (desk counter) were within 10 percent of submit-OK.

# RETURN, desk, pre-run 10

> Counts only. Submit-OK is the desk's sender log. Included is what the desk's private TN10 node accepted on chain, read by the desk counter, by accepting chain block time. Mini's files are a second read.

Payment offer 1,013 tx/s at 150 sompi/gram, from 6 payment senders, 3 per kept public node (2 unique kaspads), each its own process and connection. Families offer 1.2 hop/s, 16 families live, one family-sender process and one builder: floor (families 1–4) 100 sompi/gram on the desk's private node, double (families 5–7) 200 sompi/gram on the desk's private node, triple (families 8–10) 300 sompi/gram on the desk's private node, triple-pub (families 11–13) 300 sompi/gram on the kept public kaspads, high (families 14–16) 1000 sompi/gram on the desk's private node (public map 11:public-1,12:public-5,13:public-1).

Payment pile: 8,400 coins on the payment key at the preflight, dealt evenly over the 6 senders before the first payment (last deal, start: 8,400 coins in all, 1,400 / 1,400 / 1,400 / 1,400 / 1,400 / 1,400, even). A deal never holds more coins than the preflight pile. A coin is re-used about once a second, so one sender's ceiling is about its pool per second.

## Submit-OK and included, per minute

| Minute (UTC) | Pay submit-OK | Our payments included | Included, all non-coinbase | Counter |
|---|---:|---:|---:|---|
| 2026-11-12T07:45 | 60,789 | 60,311 | 63,911 | kept pace |
| 2026-11-12T07:46 | 60,682 | 60,692 | 64,389 | kept pace |
| 2026-11-12T07:47 | 60,734 | 61,194 | 64,809 | kept pace |

Submit-OK counts in the minute a submit was answered. Included counts in the minute of the chain block that accepted it, so a payment submitted late in one minute can be included in the next. "Kept pace" means the desk node's DAA stayed within 100 of the kept public kaspad and its sink was under 30 s old in every sample of that minute; "LAGGING" means it did not, and the count is what the node had accepted, not a network figure.

## Chain, desk counter

| Minute (UTC) | Included, all non-coinbase | Our payments included | Floor hops (100) | Double hops (200) | Triple hops (300) | Triple-pub hops (300, public) | High hops (1000) | Other traffic | Chain blocks | DAA gap max | Sink age max, ms | Final after, s | Counter |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 2026-11-12T07:45 | 63,911 | 60,311 | 4 | 21 | 48 | 52 | 138 | 3,337 | 294 | 0 | 521 | 19 | kept pace |
| 2026-11-12T07:46 | 64,389 | 60,692 | 9 | 27 | 52 | 47 | 136 | 3,426 | 316 | 2 | 468 | 20 | kept pace |
| 2026-11-12T07:47 | 64,809 | 61,194 | 2 | 17 | 48 | 52 | 136 | 3,362 | 306 | 0 | 450 | 19 | kept pace |

Coinbase is taken out as one per merged blue block (on this node a chain block's accepted list carries the coinbase of each blue block it merges). Other traffic is the rest: other users' load, the genesis, and anything not in our logs.

## Hop rate per cohort, as built

Floor (families 1–4, desk private node): 100 sompi/gram per hop. Double (families 5–7, desk private node): 200 sompi/gram per hop. Triple (families 8–10, desk private node): 300 sompi/gram per hop. Triple-pub (families 11–13, kept public kaspads): 300 sompi/gram per hop. High (families 14–16, desk private node): 1000 sompi/gram per hop. The rate rides on each hop line to the one builder. Payments pay 150.

## Funding coins, as read from the desk node

The funding coins were not one size. Sizes seen, whole tKAS (coins): 27 (648), 28 (638), 29 (637), 26 (541), 30 (523), 25 (418), 31 (412), 32 (309), 24 (287), 33 (196), 23 (187), 34 (127), and 64 more sizes. The fee is not called the whole cause.

## Minutes

| Minute (UTC) | Pay submit-OK | Attempts | Rejects, rate | Rejects, full | Other | Floor OK / att / rate rej / full rej / waiting | Double OK / att / rate rej / full rej / waiting | Triple OK / att / rate rej / full rej / waiting | Triple-pub OK / att / rate rej / full rej / waiting | High OK / att / rate rej / full rej / waiting | Family stalls logged | Family node mempool-high marks | Clean |
|---|---:|---:|---:|---:|---:|---|---|---|---|---|---:|---:|---|
| 2026-11-12T07:45 | 60,789 | 60,789 | 0 | 0 | 0 | 4 / 283 / 0 / 0 / 4 | 20 / 222 / 0 / 0 / 2 | 47 / 235 / 0 / 0 / 2 | 52 / 234 / 0 / 0 / 13 | 136 / 272 / 0 / 0 / 1 | 1 | 0 | yes |
| 2026-11-12T07:46 | 60,682 | 60,682 | 0 | 0 | 0 | 9 / 287 / 0 / 0 / 4 | 28 / 223 / 0 / 0 / 3 | 53 / 238 / 0 / 0 / 3 | 47 / 233 / 0 / 0 / 13 | 138 / 276 / 0 / 0 / 3 | 1 | 0 | yes |
| 2026-11-12T07:47 | 60,734 | 60,734 | 0 | 0 | 0 | 2 / 285 / 0 / 0 / 4 | 17 / 221 / 0 / 0 / 3 | 46 / 233 / 0 / 0 / 1 | 51 / 231 / 0 / 0 / 12 | 133 / 266 / 0 / 0 / 0 | 3 | 0 | yes |

A family stall is a coordinator mark: no hop of that family landed for a while. The family was still attempting. It is logged, and it does not make the minute dirty.

A mempool-high mark means the family node read a mempool at or over 90,000. In pre-run 10 that does not stop the families: the skip does not apply to them. A skip, if one were set, is dirt with its reason (node-skip-fam) for every minute it covers, and it clears when the mempool falls back under the line.

Within 10 percent means 54,702 to 66,858 submit-OK in the minute.

## Public nodes (local numbers)

Kept: 1, 5. The family sender reads and submits floor, double, triple and high on the desk's private node, which takes no payment submit and which the desk counter reads; triple-pub (11:public-1,12:public-5,13:public-1) reads and submits on kept public kaspads, the payments' nodes.

Kept nodes are unique kaspads: each answered with its own node id at the preflight. 3 candidate endpoints passed the check and were 2 kaspads (node 4 is node 1; the second hostname was not used). 3 payment senders per kaspad.

| Node | Synced every sample | Last DAA | Pay submit-OK | Pay rejects | Dropped sockets | Answer ms, median |
|---:|---|---:|---:|---:|---:|---:|
| 1 | yes | 621333868 | 91,048 | 0 | 0 | 37 |
| 5 | yes | 621333868 | 91,157 | 0 | 0 | 38 |

## Payment senders

| Sender | Node | Pay submit-OK | Rejects | Minutes with a row |
|---|---:|---:|---:|---:|
| 1.1 | 1 | 30,345 | 0 | 3 of 3 |
| 1.2 | 1 | 30,324 | 0 | 3 of 3 |
| 1.3 | 1 | 30,379 | 0 | 3 of 3 |
| 5.1 | 5 | 30,347 | 0 | 3 of 3 |
| 5.2 | 5 | 30,503 | 0 | 3 of 3 |
| 5.3 | 5 | 30,307 | 0 | 3 of 3 |

## Hop submit to landing, per cohort

| Cohort | Landed of OK | Median ms | Slow tail (p95) ms |
|---|---:|---:|---:|
| floor | 11 of 15 | 30242 | 79654 |
| double | 65 of 65 | 5649 | 23670 |
| triple | 146 of 146 | 3009 | 7690 |
| triple-pub | 150 of 150 | 2897 | 8656 |
| high | 407 of 407 | 1141 | 1710 |

Landing is the accepting block header time the desk's coordinator read. Waiting is submitted-OK not yet landed at the minute's end. Triple and triple-pub pay the same rate; they differ only in the node a hop is read and submitted on.
