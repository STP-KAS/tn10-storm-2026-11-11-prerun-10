> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md) · This page does not start a machine. Pre-run 10. Not Wednesday. Not Tuesday. Not pre-run 1, 2, 3, 4, 5, 6, 7, 8, or 9.

# Targets

There is no T0. There is no public clock. There is no latest minute. A scored target stays until three clean minutes land, or until one repair pass is done.

The hash file comes first and does not wait for the paste (see Order, step 2). Nothing else in this page starts until the gates are true: Mini's TN10 node is synced with DAA moving and Mini has notified Build and TN10 ops; the desk's private TN10 node is up from its own data (PowerShell 7, no wipe) and synced; no Tuesday, Wednesday, pre-run 1, 2, 3, 4, 5, 6, 7, 8, or 9 runner is up; the operator has armed (no paste; see the README); and this repo's `logs/PRE-RUN-OPEN.md` is on origin.

## Order

1. **Nodes live.** Both TN10 nodes synced, DAA moving. No wipe.
2. **Hashes first.** [hashes/SIXTEEN.md](../hashes/README.md): sixteen rows, family label, cohort, sha256 of the lowercase hex covenant id, and an On origin line. It is written before the paste and is not an arm or a send. No On origin line, no family submit. The old 8- or 32-family publisher is not used.
3. **Families.** The sixteen covenant families start.
4. **Senders, step by step.** The payment offers below, in order.

| Order | Offer, tx/s | Who sends | File | Kind |
|---:|---:|---|---|---|
| 1 | 1,013 | desk | HOLD-1 | scored |
| 2 | 1,500 | desk | HOLD-2 | scored |
| 3 | 1,800 | desk | HOLD-3 | scored |
| 4 | 1,013 | desk, and the bot if a free synced node answers | HOLD-4 | observation |
| 5 | 1,013 | desk | RETURN | scored |

Sixteen families, offer 1.2 hop/s, boson, stagger 0, from the first family submit until RETURN closes. Five cohorts, one build, one family-sender process:

| Cohort | Families | Rate, sompi/gram | Fee per hop (mass 13,046) | Submit path |
|---|---|---:|---:|---|
| floor | 1–4 | 100 | 1,304,600 | desk private node |
| double | 5–7 | 200 | 2,609,200 | desk private node |
| triple | 8–10 | 300 | 3,913,800 | desk private node |
| triple-pub | 11–13 | 300 | 3,913,800 | kept public kaspads, round-robin |
| high | 14–16 | 1000 | 13,046,000 | desk private node |

Payments pay 150. Genesis 200. In the one builder the rate rides on each hop, so a hop's fee is its mass times its family's rate ([tools/sixteen](../tools/sixteen/README.md#hop-fees)). A single rate for the process is not a fee difference. A second builder is not the fix. If the funding coins are not one size, the file says so and does not call the fee the whole cause.

A scored minute is clean when the desk's submit path is synced, that node's DAA is moving, submit-OK is within 10 percent, rejects are logged as rate or full, no sender-off, pool-low, node-drop, or proc-exit, and every family is still attempting, and no family-node skip is on (a skip is dirt with its reason for every minute it covers). A family STALL mark (no hop of that family landing for a while) is logged per minute. It is not dirt: the family is still attempting. A stall at the two-thirds rate is part of the congestion question. Mini's marks do not gate the next offer. The desk counter's inclusion figures are reported next to submit-OK in every file; they are not scored (lock line (iv)).

Payment senders use every public node that answers synced: three processes per kept unique kaspad, each its own connection (lock line (iii)). The desk keeps that set through HOLD-4. The family sender is on the desk's private TN10 node, which takes no payment submit (lock line (i)), except triple-pub, which reads, catches up and submits on the kept public kaspads.

HOLD-4 opens when the desk's HOLD-3 file is on origin, met or `NOT MET`. The sample minute is the first whole UTC minute whose start is at least 3 minutes after that file's On origin time. The desk's rate in that minute is 1,013: the runner drops the payment rate to 1,013 as soon as HOLD-3 is scored. If the path is not synced, the file still covers that minute and says so. The run does not open a later minute. This pinned minute is a target rule inside the run. It is not a public clock.

The bot uses one public node outside the desk's HOLD-3 set. The split stays in the local config. The config is not committed. No free synced node means the bot does not send.

The abort line stays **2,500 coins** and **18,000 usable tKAS**. Do not lower it. Do not spend a coin at or above 100,000 tKAS. If this pre-run would leave the lane under that line, do not start.

The desk node process is not stopped by this pre-run. No chain data is wiped on any machine.

The Wednesday pages stay as they are. Pre-run 1's pages stay as they are. This page is pre-run 10's page.

Locks: [locks/LOCKED.md](../locks/LOCKED.md).

## Why this shape

> This is our own TN10 testing. The figures below are what we observed in earlier pre-runs on our own nodes, not claims about how TN10 behaves in general.

In pre-runs 8 and 9 we observed blocks taking about 110,000–132,000 transactions a minute (roughly 1,800–2,200 tx/s) when pushed. In pre-run 9, HOLD-2 at 1,800 tx/s was included as sent, yet the chained low-fee families had already slowed: floor (100) fell to about 13 percent of its HOLD-1 hop rate, double (200) to about 25 percent, triple (300) to about 38 percent, while high (1000) kept about 92 percent. We did not have a step below 1,800, so we could not say where the slowdown starts.

So pre-run 10 changes only the offer ladder:

- **HOLD-1 at 1,013** is the baseline, as before.
- **HOLD-2 at 1,500 and HOLD-3 at 1,800 are the two measured steps.** 1,500 is about 70–80 percent of the block space we observed; 1,800 repeats pre-run 9's HOLD-2 so the two runs can be compared. Reading the hop rate per cohort at both should show whether cheap chains already slow at 1,500, or only near 1,800.
- **No step goes over capacity.** Pre-run 9's 2,500 step is dropped. In pre-run 8 our long over-capacity stretch crowded out other TN10 users; pre-run 9 already had its over-capacity reading. The rate drops back to 1,013 as soon as HOLD-3 is scored; HOLD-4 (observation) and RETURN stay at 1,013.
- **Cohorts, fees and paths are pre-run 9's, unchanged** (floor 100, double 200, triple 300 on the desk node, triple-pub 300 on the public kaspads, high 1000). Keeping them the same keeps the two runs comparable, and keeps one same-fee pair on two paths (triple and triple-pub), so a path effect can still be told apart from a fee effect. We chose this over putting every cohort on one path because the pair gave pre-run 9's cleanest single reading and costs nothing extra.

## Selection rule

Read before the run, in rusty-kaspa tag v2.1.0, commit `01b532e8b553523216471682649693af92f0fd16`. Every kaspad in use answered version 2.1.0 in pre-runs 8 and 9.

- `mining/src/mempool/model/frontier.rs`, `build_selector` (line 379): if the ready transactions fit in one block (`total_mass <= max_block_mass`) the template takes them all, best feerate first (`TakeAllSelector`). If they are more than four blocks' worth (`COLLISION_FACTOR = 4`, line 31) it samples at random (`sample_inplace`, line 249). In between it uses `MutatingTreeSelector`, random selection without replacement.
- `mining/src/mempool/model/frontier/feerate_key.rs` line 31: each ready transaction's weight is `(fee / mass)^ALPHA`; `ALPHA = 3` in `frontier/selectors.rs` line 18. So once the ready set is larger than a block, the chance of being picked goes with the cube of the feerate. Against payments at 150, a hop at 100 weighs about 0.3, at 200 about 2.4, at 300 about 8, at 1000 about 296.
- `mining/src/mempool/model/transactions_pool.rs` lines 124–128 and 156–159: only a transaction with no parent in the mempool is ready. A child becomes ready when its last in-mempool parent leaves. Each family is a chain of hops, so a hop waits for its parent whatever its fee.
- `mining/src/mempool/config.rs` line 3: the default pool holds up to 1,000,000 transactions.

What this suggests, before any count: under capacity every ready transaction should be taken, so the tiers should land alike. Over capacity a higher fee should raise the odds per block without guaranteeing a place, so 300 and 1000 should still land, slower than under capacity, and 100 should slow most. Caveats: the run sees no miner's template; the mempool feerate uses normalised mass; the funding coins are not one size.
