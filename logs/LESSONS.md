> **Experimental. We are just trying this.** [Disclaimer](../DISCLAIMER.md) · Kaspa Testnet-10 only; tKAS has no value. Pre-run 10.
>
> **Our own testing.** This is our own Kaspa Testnet-10 testing, run on our own machines and nodes. What this page reports is what we observed in this run; it is not a claim of how TN10 or Kaspa behave in general.

# Lessons, pre-run 10

> Written by the operator after RETURN closed and the counter's tail was read. [METHOD.md](METHOD.md) is the desk runner's own summary; its last section, the reading against the selection rule, was added by the operator afterwards. Included counts are the desk counter's read of the desk's private TN10 node ([counts/chain/TIMELINE.md](../counts/chain/TIMELINE.md)), checked against a kept public kaspad every 10 s. They are one node's view of the accepted chain, not a network-wide figure. The run sees no miner's template, so anything below about how templates picked transactions is inferred, not read.

## What happened

Every step closed on its first three minutes, with no repair. The runner was not restarted, nothing was killed, and no `FAILED` file was written. Every desk count file, the timeline, the method file, and the bot's file reached origin on the first try. The desk node was not stopped.

MET below means desk submit-OK, as scored. Inclusion is reported next to it, not scored.

| Step | Offer, tx/s | Desk head | Submit-OK per scored minute | Our payments included, same minutes | Payments included within 10 percent | Desk file on origin (UTC), commit |
|---|---:|---|---|---|---|---|
| HOLD-1 | 1,013 | MET | 60,883 / 60,839 / 60,621 | 61,168 / 60,306 / 61,357 | 3 of 3 | 07:31:22Z, 1ad5c81 |
| HOLD-2 | 1,500 | MET | 89,709 / 90,527 / 90,041 | 89,942 / 91,339 / 90,280 | 3 of 3 | 07:35:22Z, 754a914 |
| HOLD-3 | 1,800 | MET | 108,049 / 107,820 / 108,111 | 106,471 / 106,500 / 113,456 | 3 of 3 | 07:39:22Z, 4cc7a99 |
| HOLD-4 | 1,013 | OBSERVATION | 60,772 (pinned minute 07:43Z) | 61,025 | 1 of 1 | 07:44:22Z, ba1f8da |
| RETURN | 1,013 | MET | 60,789 / 60,682 / 60,734 | 60,311 / 60,692 / 61,194 | 3 of 3 | 07:48:22Z, bafa32d |

The payment rate fell back to 1,013 at 07:39:12Z, as HOLD-3 was scored. No step was offered over the block space we had observed in pre-runs 8 and 9. The bot filed `NO SEND no-free-node` for HOLD-4 (17ab4f8, on origin 07:44:04Z): in its pass at 07:42:30Z every answering endpoint was one of the desk's two kept kaspads. The timeline (61ad119, 07:53:33Z) and the runner's method file (d74106f, 07:53:36Z) followed the 5-minute tail; the desk runner ended at 07:53:38Z. Mini published a second read for every step.

## Hops per cohort

Hops included per scored minute, desk counter (sums of the scored minutes). Floor has four families, the other cohorts three, so floor's column is per four families. Pre-run 9's HOLD-1, at the same 1,013 offer, is shown for comparison.

| Step | Floor 100 (4 fam.) | Double 200 | Triple 300, desk | Triple-pub 300, public | High 1000 |
|---|---:|---:|---:|---:|---:|
| Pre-run 9 HOLD-1 | 373 | 302 | 343 | 458 | 420 |
| HOLD-1 (1,013) | 20 | 52 | 148 | 153 | 402 |
| HOLD-2 (1,500) | 1 | 20 | 76 | 81 | 371 |
| HOLD-3 (1,800) | 1 | 8 | 44 | 49 | 328 |
| HOLD-4 (1,013, one minute) | 5 | 25 | 57 | 59 | 135 |
| RETURN (1,013) | 15 | 65 | 148 | 151 | 410 |

Median submit-to-landing per hop, seconds (p95 in brackets), from the step files:

| Step | Floor | Double | Triple | Triple-pub | High |
|---|---|---|---|---|---|
| HOLD-1 | 14.0 (114.9) | 7.7 (29.1) | 2.8 (7.8) | 2.6 (8.6) | 1.1 (1.8) |
| HOLD-2 | 0 of 1 landed | 19.7 (65.6) | 6.2 (16.5) | 4.1 (19.9) | 1.3 (2.0) |
| HOLD-3 | 0 of 1 landed | 19.6 (123.4), 6 of 8 | 9.1 (36.2) | 7.6 (27.0) | 1.5 (2.5) |
| HOLD-4 | 38.2 (60.8) | 5.3 (18.3) | 2.3 (9.9) | 2.2 (6.5) | 1.2 (1.8) |
| RETURN | 30.2 (79.7) | 5.6 (23.7) | 3.0 (7.7) | 2.9 (8.7) | 1.1 (1.7) |

Whole run, as read by the end of the tail: 1,607,515 payment submit-OKs, all of them included. Family hops included: floor 92, double 359, triple 888, triple-pub 955, high 2,829.

## What this seems to show

- **The counter kept pace.** Every whole minute from 07:27Z to the end of the tail was marked kept pace: DAA gap at most 3 against the kept public kaspad, sink age at most about 1.2 s, each minute final about 19–20 s after its end. No minute was `LAGGING`. The start minute (07:26Z) was partial and the last tail minute (07:53Z) not final, as marked.
- **Payments were included as sent at 1,013, 1,500 and 1,800.** HOLD-2 all non-coinbase sat at about 93,000–95,000 a minute; HOLD-3 at about 110,000–117,000, inside the 110,000–132,000 band we had observed when we pushed in pre-runs 8 and 9. In 3 of 3 scored minutes at each of those steps, our payments included were within 10 percent of submit-OK.
- **In this run, cheap chained hops were already slow at HOLD-1 1,013.** That is the main difference from pre-run 9. In pre-run 9's HOLD-1, floor landed 373 hops in three scored minutes, median 1.6 s. Here floor landed 20 (about 5 percent of that), median 14.0 s, and the first full minute (07:27Z, not scored) already had only 7 floor hops. Double was 52 against 302, median 7.7 s against 1.4 s; triple 148 against 343, median 2.8 s against 1.3 s. High was barely different: 402 against 420, median 1.1 s in both runs. So the 1,500 vs 1,800 comparison in this run starts from an already-slow cheap-tier baseline, not from the uncongested HOLD-1 we saw in pre-run 9.
- **From that baseline, the cheap tiers slowed further at 1,500 and again at 1,800, in fee order.** Against this run's own HOLD-1 scored-minute totals, floor went to 1 hop at 1,500 (5 percent) and 1 hop at 1,800; double to 38 percent then 15 percent; triple to 51 percent then 30 percent; high to 92 percent then 82 percent, and still landed every OK hop (median 1.3 s then 1.5 s). At the same 1,800 offer, pre-run 9's HOLD-2 had still landed 47 floor hops; this run's HOLD-3 landed 1. We cannot, from this run alone, say that 1,500 is where cheap chains start to slow, because they were already slow at 1,013.
- **Possible reasons for the slow HOLD-1, as hypotheses only.** Landed "other traffic" on this node was about 2,800–3,640 a minute throughout, including 3,533–3,584 in the four whole tail minutes after our payments had stopped, close to pre-run 9's 2,800–3,400 and to the about 56 tx/s base load noted elsewhere on this map. So a higher landed-other column does not show up as the difference. A backlog already waiting in mempools, or the mempool state after the family re-funding (15 fresh genesis coins at 06:56:53Z, about half an hour before the first payment), could produce a weighted-sampling frontier even while our own landed load at HOLD-1 was only about 64,000–65,000 a minute. We did not read mempool sizes or miners' templates, so these stay hypotheses.
- **RETURN did not bring the floor back to pre-run 9's uncongested rate.** After the rate dropped at 07:39:12Z, HOLD-4 (one minute) and RETURN still had floor medians of 38.2 s and 30.2 s (15 hops in three RETURN minutes). Triple, triple-pub and high returned to about this run's HOLD-1 per-minute hop counts. In pre-run 9, HOLD-4 and RETURN had already brought every tier, including floor, back to a 0.9–1.7 s median.
- **The 1000 tier was barely touched by the load.** High landed every OK hop in every step, with a median of 1.1–1.5 s.
- **Fee order held at every step, including HOLD-1.** See [METHOD.md](METHOD.md#reading-against-the-selection-rule).
- **The same-fee path gap was in the same direction as pre-run 9, and smaller.** Triple-pub (300, public) was faster than desk triple at every step (HOLD-1 median 2.6 s against 2.8 s; HOLD-3 7.6 s against 9.1 s) and landed slightly more hops (955 against 888 over the whole run). Uncongested, that gap had been about a third more hops and about 0.4 s; here both 300 cohorts were already delayed at HOLD-1.
- **Mini's one-hop-per-transaction fix matched the desk in 49 of 50 cells in HOLD-1 to HOLD-4.** The 50 cells are five cohorts in the ten scored minutes of those steps. The one mismatch is floor at 07:28Z (desk 3, Mini 2). All 15 RETURN cells matched (64 of 65 cells over the whole scored run). Mini's non-coinbase was within about 0.4 percent of the desk's (for example 65,070 against 64,812 at 07:28Z). Removals after a minute had closed: 0, logged. The desk counter stays the inclusion figure.

## Spend

- Payment fees: the pile's coin total went from 191,994.94 tKAS (pre-run 9's end snapshot, this run's start, also the six sender-pool `.used` files) to 188,079.03 tKAS (this run's end pool snapshots): 3,915.91 tKAS for 1,607,515 payments, about 0.0024 tKAS each. 8,400 coins before and after.
- Family re-funding, before hashes: `fund10.mjs` at 06:56:53Z sent 15 transactions, none rejected, one fresh genesis coin to each of keys 1–15. Those 15 outputs totaled 313.39 tKAS; fees were 0.03654 tKAS. The payment pile was not topped up. The family lane read 5,541 coins and 245,475 usable tKAS before that funding, 5,526 coins and 245,207 usable tKAS at the run preflight (07:26:10Z), and 5,526 coins and 239,622 usable tKAS when status.mjs was read after the run (08:00:37Z). From before funding to after the run that is 15 coins and 5,853 usable tKAS. It is not split further here. Keys 1–15 have no genesis coin left.
- Both stay far above the abort line (2,500 coins, 18,000 usable tKAS).

## What a next attempt could try (not opened)

1. If the question is still where cheap chains start to slow between 1,013 and 1,800, wait for a HOLD-1 in which the cheap tiers land like they did in pre-run 9, or record why they do not, before treating 1,500 and 1,800 as the first congested steps.
2. Keep one same-fee pair on two paths, which still read in the same direction, or put every cohort on one path.
3. Read the miners' side if any miner's template or mempool can be read, so a already-full frontier at 1,013 can be tested, not inferred.
4. Keep Mini's one-hop-per-transaction `classify()`, which held in 49 of 50 cells; the desk counter stays the inclusion figure.
5. The bot stays a `NO SEND` until a third unique kaspad answers.
