MET

Scored on submit-OK, not on inclusion. Inclusion, reported and not scored: in 3 of 3 minutes our payments included (desk counter) were within 10 percent of submit-OK.

# HOLD-3, desk, pre-run 10

> Counts only. Submit-OK is the desk's sender log. Included is what the desk's private TN10 node accepted on chain, read by the desk counter, by accepting chain block time. Mini's files are a second read.

Payment offer 1,800 tx/s at 150 sompi/gram, from 6 payment senders, 3 per kept public node (2 unique kaspads), each its own process and connection. Families offer 1.2 hop/s, 16 families live, one family-sender process and one builder: floor (families 1–4) 100 sompi/gram on the desk's private node, double (families 5–7) 200 sompi/gram on the desk's private node, triple (families 8–10) 300 sompi/gram on the desk's private node, triple-pub (families 11–13) 300 sompi/gram on the kept public kaspads, high (families 14–16) 1000 sompi/gram on the desk's private node (public map 11:public-1,12:public-5,13:public-1).

Payment pile: 8,400 coins on the payment key at the preflight, dealt evenly over the 6 senders before the first payment (last deal, start: 8,400 coins in all, 1,400 / 1,400 / 1,400 / 1,400 / 1,400 / 1,400, even). A deal never holds more coins than the preflight pile. A coin is re-used about once a second, so one sender's ceiling is about its pool per second.

## Submit-OK and included, per minute

| Minute (UTC) | Pay submit-OK | Our payments included | Included, all non-coinbase | Counter |
|---|---:|---:|---:|---|
| 2026-11-12T07:36 | 108,049 | 106,471 | 109,677 | kept pace |
| 2026-11-12T07:37 | 107,820 | 106,500 | 109,627 | kept pace |
| 2026-11-12T07:38 | 108,111 | 113,456 | 116,838 | kept pace |

Submit-OK counts in the minute a submit was answered. Included counts in the minute of the chain block that accepted it, so a payment submitted late in one minute can be included in the next. "Kept pace" means the desk node's DAA stayed within 100 of the kept public kaspad and its sink was under 30 s old in every sample of that minute; "LAGGING" means it did not, and the count is what the node had accepted, not a network figure.

## Chain, desk counter

| Minute (UTC) | Included, all non-coinbase | Our payments included | Floor hops (100) | Double hops (200) | Triple hops (300) | Triple-pub hops (300, public) | High hops (1000) | Other traffic | Chain blocks | DAA gap max | Sink age max, ms | Final after, s | Counter |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 2026-11-12T07:36 | 109,677 | 106,471 | 1 | 4 | 12 | 17 | 108 | 3,064 | 269 | 1 | 1056 | 20 | kept pace |
| 2026-11-12T07:37 | 109,627 | 106,500 | 0 | 2 | 13 | 17 | 98 | 2,997 | 267 | 0 | 1076 | 20 | kept pace |
| 2026-11-12T07:38 | 116,838 | 113,456 | 0 | 2 | 19 | 15 | 122 | 3,224 | 300 | 0 | 487 | 19 | kept pace |

Coinbase is taken out as one per merged blue block (on this node a chain block's accepted list carries the coinbase of each blue block it merges). Other traffic is the rest: other users' load, the genesis, and anything not in our logs.

## Hop rate per cohort, as built

Floor (families 1–4, desk private node): 100 sompi/gram per hop. Double (families 5–7, desk private node): 200 sompi/gram per hop. Triple (families 8–10, desk private node): 300 sompi/gram per hop. Triple-pub (families 11–13, kept public kaspads): 300 sompi/gram per hop. High (families 14–16, desk private node): 1000 sompi/gram per hop. The rate rides on each hop line to the one builder. Payments pay 150.

## Funding coins, as read from the desk node

The funding coins were not one size. Sizes seen, whole tKAS (coins): 29 (720), 28 (667), 27 (632), 30 (617), 26 (458), 31 (444), 32 (348), 25 (332), 33 (249), 24 (215), 34 (143), 23 (132), and 63 more sizes. The fee is not called the whole cause.

## Minutes

| Minute (UTC) | Pay submit-OK | Attempts | Rejects, rate | Rejects, full | Other | Floor OK / att / rate rej / full rej / waiting | Double OK / att / rate rej / full rej / waiting | Triple OK / att / rate rej / full rej / waiting | Triple-pub OK / att / rate rej / full rej / waiting | High OK / att / rate rej / full rej / waiting | Family stalls logged | Family node mempool-high marks | Clean |
|---|---:|---:|---:|---:|---:|---|---|---|---|---|---:|---:|---|
| 2026-11-12T07:36 | 108,049 | 108,049 | 0 | 0 | 0 | 1 / 282 / 0 / 0 / 4 | 4 / 216 / 0 / 0 / 3 | 12 / 217 / 0 / 0 / 3 | 17 / 220 / 0 / 0 / 13 | 109 / 260 / 0 / 0 / 3 | 3 | 0 | yes |
| 2026-11-12T07:37 | 107,820 | 107,820 | 0 | 0 | 0 | 0 / 283 / 0 / 0 / 4 | 2 / 213 / 0 / 0 / 3 | 13 / 218 / 0 / 0 / 3 | 18 / 220 / 0 / 0 / 14 | 98 / 256 / 0 / 0 / 3 | 2 | 0 | yes |
| 2026-11-12T07:38 | 108,111 | 108,111 | 0 | 0 | 0 | 0 / 283 / 0 / 0 / 4 | 2 / 213 / 0 / 0 / 3 | 19 / 219 / 0 / 0 / 3 | 14 / 214 / 0 / 0 / 13 | 122 / 270 / 0 / 0 / 3 | 2 | 0 | yes |

A family stall is a coordinator mark: no hop of that family landed for a while. The family was still attempting. It is logged, and it does not make the minute dirty.

A mempool-high mark means the family node read a mempool at or over 90,000. In pre-run 10 that does not stop the families: the skip does not apply to them. A skip, if one were set, is dirt with its reason (node-skip-fam) for every minute it covers, and it clears when the mempool falls back under the line.

Within 10 percent means 97,200 to 118,800 submit-OK in the minute.

## Public nodes (local numbers)

Kept: 1, 5. The family sender reads and submits floor, double, triple and high on the desk's private node, which takes no payment submit and which the desk counter reads; triple-pub (11:public-1,12:public-5,13:public-1) reads and submits on kept public kaspads, the payments' nodes.

Kept nodes are unique kaspads: each answered with its own node id at the preflight. 3 candidate endpoints passed the check and were 2 kaspads (node 4 is node 1; the second hostname was not used). 3 payment senders per kaspad.

| Node | Synced every sample | Last DAA | Pay submit-OK | Pay rejects | Dropped sockets | Answer ms, median |
|---:|---|---:|---:|---:|---:|---:|
| 1 | yes | 621328674 | 162,384 | 0 | 0 | 40 |
| 5 | yes | 621328674 | 161,596 | 0 | 0 | 38 |

## Payment senders

| Sender | Node | Pay submit-OK | Rejects | Minutes with a row |
|---|---:|---:|---:|---:|
| 1.1 | 1 | 54,149 | 0 | 3 of 3 |
| 1.2 | 1 | 54,100 | 0 | 3 of 3 |
| 1.3 | 1 | 54,135 | 0 | 3 of 3 |
| 5.1 | 5 | 53,877 | 0 | 3 of 3 |
| 5.2 | 5 | 53,855 | 0 | 3 of 3 |
| 5.3 | 5 | 53,864 | 0 | 3 of 3 |

## Hop submit to landing, per cohort

| Cohort | Landed of OK | Median ms | Slow tail (p95) ms |
|---|---:|---:|---:|
| floor | 0 of 1 | - | - |
| double | 6 of 8 | 19570 | 123399 |
| triple | 44 of 44 | 9119 | 36224 |
| triple-pub | 49 of 49 | 7617 | 26956 |
| high | 329 of 329 | 1463 | 2534 |

Landing is the accepting block header time the desk's coordinator read. Waiting is submitted-OK not yet landed at the minute's end. Triple and triple-pub pay the same rate; they differ only in the node a hop is read and submitted on.
