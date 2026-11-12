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
