# Method, pre-run 10

> This is our own Kaspa Testnet-10 testing. What follows is what we observed in this run, on our own nodes; it is not a claim of how TN10 or Kaspa behave in general.

> Counts only. Desk side. Submit-OK is the desk sender log; included is the desk counter's read of what the desk's private TN10 node accepted on chain. Mini's files are a second read.

Accepted hops per cohort, as the desk's coordinator read them: floor 88, double 356, triple 885, triple-pub 942, high 2,826.

Payment submit-OK and included per scored minute:

- HOLD-1: MET on submit-OK, submit-OK 60,883 / 60,839 / 60,621; our payments included 61,168 / 60,306 / 61,357; hops included floor/double/triple/triple-pub/high 20/52/148/153/402; counter minutes not kept-pace 0 of 3.
- HOLD-2: MET on submit-OK, submit-OK 89,709 / 90,527 / 90,041; our payments included 89,942 / 91,339 / 90,280; hops included floor/double/triple/triple-pub/high 1/20/76/81/371; counter minutes not kept-pace 0 of 3.
- HOLD-3: MET on submit-OK, submit-OK 108,049 / 107,820 / 108,111; our payments included 106,471 / 106,500 / 113,456; hops included floor/double/triple/triple-pub/high 1/8/44/49/328; counter minutes not kept-pace 0 of 3.
- HOLD-4: OBSERVATION, submit-OK 60,772; our payments included 61,025; hops included floor/double/triple/triple-pub/high 5/25/57/59/135; counter minutes not kept-pace 0 of 1.
- RETURN: MET on submit-OK, submit-OK 60,789 / 60,682 / 60,734; our payments included 60,311 / 60,692 / 61,194; hops included floor/double/triple/triple-pub/high 15/65/148/151/410; counter minutes not kept-pace 0 of 3.

Decent on the desk side: HOLD-1 met.

## Selection rule, read before the run

The desk node and the kept public kaspads answered serverVersion 2.1.0 at the preflight. In rusty-kaspa tag v2.1.0 (commit 01b532e8b553523216471682649693af92f0fd16), `mining/src/mempool/model/frontier.rs` `build_selector` takes every ready transaction best-first while the ready set's mass fits one block, and otherwise samples at random with weight (fee/mass)^3 (`ALPHA = 3` in `mining/src/mempool/model/frontier/selectors.rs`, weight in `mining/src/mempool/model/frontier/feerate_key.rs`): `sample_inplace` above four blocks' mass, `MutatingTreeSelector` between one and four. Only a transaction with no parent in the mempool is in the ready set (`mining/src/mempool/model/transactions_pool.rs`), so a chained hop is not a candidate until its parent is out of the mempool. Against payments at 150, the weights are 0.30 (100), 2.4 (200), 8 (300) and 296 (1000). A higher fee raises the odds; it does not buy a place in a queue. This is the source's rule, read from the code; the run does not see a miner's template.

Hop rates per hop, one builder: floor (families 1–4) 100 sompi/gram on the desk's private node, double (families 5–7) 200 sompi/gram on the desk's private node, triple (families 8–10) 300 sompi/gram on the desk's private node, triple-pub (families 11–13) 300 sompi/gram on the kept public kaspads, high (families 14–16) 1000 sompi/gram on the desk's private node. Payments 150. The funding coins were not one size, so the fee is not called the whole cause. Triple-pub (11:public-1,12:public-5,13:public-1) was read and submitted on the kept public kaspads; every other cohort on the desk's private TN10 node, which took no payment submit and also ran the counter. Payments: 6 senders, 3 per kept kaspad, 2 unique kaspads, pile 8,400 coins.

## Misses

- none

## Fixes

- none

## On origin

- counts/desk/HOLD-1.md: 2026-11-12T07:31:22Z
- counts/desk/HOLD-2.md: 2026-11-12T07:35:22Z
- counts/desk/HOLD-3.md: 2026-11-12T07:39:22Z
- counts/desk/HOLD-4.md: 2026-11-12T07:44:22Z
- counts/desk/RETURN.md: 2026-11-12T07:48:22Z
- counts/chain/TIMELINE.md: 2026-11-12T07:53:33Z

## Reading against the selection rule

Added by the operator after the run; the runner's text above is unchanged. Figures are from the step files and [counts/chain/TIMELINE.md](../counts/chain/TIMELINE.md). The run sees no miner's template, so this is a fit to the rule as read in the source, not a measurement of it. These are observations from this run, not a claim about every TN10 miner.

Rule, as cited above: rusty-kaspa v2.1.0 (01b532e8), `frontier.rs` `build_selector`; weight (fee/mass)^3 with `ALPHA = 3` in `selectors.rs`; only transactions with no parent in the mempool are in the frontier. Against payments at 150 sompi/gram the weights are 0.30 (floor, 100), 2.4 (double, 200), 8 (triple and triple-pub, 300) and 296 (high, 1000).

- **HOLD-1 did not look like the take-all branch we saw in pre-run 9.** In pre-run 9, under capacity (HOLD-1, HOLD-4, RETURN) every cohort landed in 0.9–1.7 s and every OK hop landed. In this run, at the same 1,013 offer, landing already followed the weight order: high 1.1 s (402 hops), triple-pub 2.6 s, triple 2.8 s, double 7.7 s, floor 14.0 s (20 hops, and 16 of 20 landed). That is the shape we associated in pre-run 9 with a frontier that no longer fits in one block. Our own landed load at HOLD-1 was only about 64,000–65,000 non-coinbase a minute, well under the 110,000–132,000 band from pre-runs 8 and 9, so the fit, if it holds, points at transactions already waiting that we did not land in the "other traffic" column, not at the size of our own offer. That is a hypothesis, not a reading of a mempool or a template.
- **At 1,500 and 1,800, landing stayed in the same weight order, and the cheap tiers slowed further.** High was barely touched (1.3 s median in HOLD-2, 1.5 s in HOLD-3; 92 and 82 percent of this run's HOLD-1 hop rate). Floor landed 0 of 1 OK hop in each of those steps. The gaps are again smaller than a pure 1/weight scaling of the extra wait, as in pre-run 9.
- **Chained hops are hit harder than single payments, as the parentless rule implies.** Payments were included as sent at all three offers. A family has one ready transaction at a time. That fits a slow floor whose head sits waiting (the waiting column in the step files) while payments at 150 keep landing.
- **Same fee, different path.** Triple and triple-pub have the same weight. Triple-pub was faster at every step and landed 955 hops against 888 over the run. The rule does not explain that difference; the node path may. The gap is smaller than in pre-run 9, where both 300 cohorts were uncongested at HOLD-1.
- **What the rule does not cover here.** Funding coins were not one size, the mempool's feerate uses normalised mass, and some miners may not run this rusty-kaspa version. The fee is not called the whole cause. We did not establish why HOLD-1 in this run already looked congested for the cheap tiers.
