MET

Scored on submit-OK, not on inclusion. Inclusion, reported and not scored: in 3 of 3 minutes our payments included (desk counter) were within 10 percent of submit-OK.

# HOLD-2, desk, pre-run 10

> Counts only. Submit-OK is the desk's sender log. Included is what the desk's private TN10 node accepted on chain, read by the desk counter, by accepting chain block time. Mini's files are a second read.

Payment offer 1,500 tx/s at 150 sompi/gram, from 6 payment senders, 3 per kept public node (2 unique kaspads), each its own process and connection. Families offer 1.2 hop/s, 16 families live, one family-sender process and one builder: floor (families 1–4) 100 sompi/gram on the desk's private node, double (families 5–7) 200 sompi/gram on the desk's private node, triple (families 8–10) 300 sompi/gram on the desk's private node, triple-pub (families 11–13) 300 sompi/gram on the kept public kaspads, high (families 14–16) 1000 sompi/gram on the desk's private node (public map 11:public-1,12:public-5,13:public-1).

Payment pile: 8,400 coins on the payment key at the preflight, dealt evenly over the 6 senders before the first payment (last deal, start: 8,400 coins in all, 1,400 / 1,400 / 1,400 / 1,400 / 1,400 / 1,400, even). A deal never holds more coins than the preflight pile. A coin is re-used about once a second, so one sender's ceiling is about its pool per second.

## Submit-OK and included, per minute

| Minute (UTC) | Pay submit-OK | Our payments included | Included, all non-coinbase | Counter |
|---|---:|---:|---:|---|
| 2026-11-12T07:32 | 89,709 | 89,942 | 93,311 | kept pace |
| 2026-11-12T07:33 | 90,527 | 91,339 | 94,922 | kept pace |
| 2026-11-12T07:34 | 90,041 | 90,280 | 93,603 | kept pace |

Submit-OK counts in the minute a submit was answered. Included counts in the minute of the chain block that accepted it, so a payment submitted late in one minute can be included in the next. "Kept pace" means the desk node's DAA stayed within 100 of the kept public kaspad and its sink was under 30 s old in every sample of that minute; "LAGGING" means it did not, and the count is what the node had accepted, not a network figure.

## Chain, desk counter

| Minute (UTC) | Included, all non-coinbase | Our payments included | Floor hops (100) | Double hops (200) | Triple hops (300) | Triple-pub hops (300, public) | High hops (1000) | Other traffic | Chain blocks | DAA gap max | Sink age max, ms | Final after, s | Counter |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 2026-11-12T07:32 | 93,311 | 89,942 | 0 | 5 | 19 | 22 | 118 | 3,205 | 260 | 1 | 774 | 20 | kept pace |
| 2026-11-12T07:33 | 94,922 | 91,339 | 0 | 8 | 35 | 39 | 126 | 3,375 | 313 | 1 | 348 | 20 | kept pace |
| 2026-11-12T07:34 | 93,603 | 90,280 | 1 | 7 | 22 | 20 | 127 | 3,148 | 286 | 1 | 683 | 20 | kept pace |

Coinbase is taken out as one per merged blue block (on this node a chain block's accepted list carries the coinbase of each blue block it merges). Other traffic is the rest: other users' load, the genesis, and anything not in our logs.

## Hop rate per cohort, as built

Floor (families 1–4, desk private node): 100 sompi/gram per hop. Double (families 5–7, desk private node): 200 sompi/gram per hop. Triple (families 8–10, desk private node): 300 sompi/gram per hop. Triple-pub (families 11–13, kept public kaspads): 300 sompi/gram per hop. High (families 14–16, desk private node): 1000 sompi/gram per hop. The rate rides on each hop line to the one builder. Payments pay 150.

## Funding coins, as read from the desk node

The funding coins were not one size. Sizes seen, whole tKAS (coins): 29 (742), 28 (668), 30 (648), 27 (595), 31 (471), 26 (452), 32 (356), 25 (314), 33 (251), 24 (195), 34 (152), 23 (117), and 64 more sizes. The fee is not called the whole cause.

## Minutes

| Minute (UTC) | Pay submit-OK | Attempts | Rejects, rate | Rejects, full | Other | Floor OK / att / rate rej / full rej / waiting | Double OK / att / rate rej / full rej / waiting | Triple OK / att / rate rej / full rej / waiting | Triple-pub OK / att / rate rej / full rej / waiting | High OK / att / rate rej / full rej / waiting | Family stalls logged | Family node mempool-high marks | Clean |
|---|---:|---:|---:|---:|---:|---|---|---|---|---|---:|---:|---|
| 2026-11-12T07:32 | 89,709 | 89,709 | 0 | 0 | 0 | 0 / 283 / 0 / 0 / 4 | 5 / 214 / 0 / 0 / 3 | 18 / 219 / 0 / 0 / 2 | 22 / 221 / 0 / 0 / 13 | 118 / 265 / 0 / 0 / 3 | 3 | 0 | yes |
| 2026-11-12T07:33 | 90,527 | 90,527 | 0 | 0 | 0 | 0 / 281 / 0 / 0 / 4 | 8 / 216 / 0 / 0 / 3 | 36 / 226 / 0 / 0 / 3 | 39 / 229 / 0 / 0 / 13 | 126 / 269 / 0 / 0 / 3 | 1 | 0 | yes |
| 2026-11-12T07:34 | 90,041 | 90,041 | 0 | 0 | 0 | 1 / 285 / 0 / 0 / 4 | 7 / 214 / 0 / 0 / 3 | 22 / 222 / 0 / 0 / 3 | 20 / 219 / 0 / 0 / 13 | 127 / 270 / 0 / 0 / 2 | 0 | 0 | yes |

A family stall is a coordinator mark: no hop of that family landed for a while. The family was still attempting. It is logged, and it does not make the minute dirty.

A mempool-high mark means the family node read a mempool at or over 90,000. In pre-run 10 that does not stop the families: the skip does not apply to them. A skip, if one were set, is dirt with its reason (node-skip-fam) for every minute it covers, and it clears when the mempool falls back under the line.

Within 10 percent means 81,000 to 99,000 submit-OK in the minute.

## Public nodes (local numbers)

Kept: 1, 5. The family sender reads and submits floor, double, triple and high on the desk's private node, which takes no payment submit and which the desk counter reads; triple-pub (11:public-1,12:public-5,13:public-1) reads and submits on kept public kaspads, the payments' nodes.

Kept nodes are unique kaspads: each answered with its own node id at the preflight. 3 candidate endpoints passed the check and were 2 kaspads (node 4 is node 1; the second hostname was not used). 3 payment senders per kaspad.

| Node | Synced every sample | Last DAA | Pay submit-OK | Pay rejects | Dropped sockets | Answer ms, median |
|---:|---|---:|---:|---:|---:|---:|
| 1 | yes | 621326572 | 135,131 | 0 | 0 | 37 |
| 5 | yes | 621326574 | 135,146 | 0 | 0 | 38 |

## Payment senders

| Sender | Node | Pay submit-OK | Rejects | Minutes with a row |
|---|---:|---:|---:|---:|
| 1.1 | 1 | 45,112 | 0 | 3 of 3 |
| 1.2 | 1 | 45,113 | 0 | 3 of 3 |
| 1.3 | 1 | 44,906 | 0 | 3 of 3 |
| 5.1 | 5 | 45,115 | 0 | 3 of 3 |
| 5.2 | 5 | 44,902 | 0 | 3 of 3 |
| 5.3 | 5 | 45,129 | 0 | 3 of 3 |

## Hop submit to landing, per cohort

| Cohort | Landed of OK | Median ms | Slow tail (p95) ms |
|---|---:|---:|---:|
| floor | 0 of 1 | - | - |
| double | 20 of 20 | 19727 | 65608 |
| triple | 76 of 76 | 6202 | 16512 |
| triple-pub | 81 of 81 | 4140 | 19882 |
| high | 371 of 371 | 1269 | 1969 |

Landing is the accepting block header time the desk's coordinator read. Waiting is submitted-OK not yet landed at the minute's end. Triple and triple-pub pay the same rate; they differ only in the node a hop is read and submitted on.
