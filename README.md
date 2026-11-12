> **Experimental. We are just trying this.** [Disclaimer](DISCLAIMER.md) · Kaspa Testnet-10 only; tKAS has no value.
>
> **This is a pre-run. Pre-run 10.** It is not the Wednesday run. It is not the Tuesday run. It is not pre-run 1, 2, 3, 4, 5, 6, 7, 8, or 9. A read does not start a runner.

# tn10-storm-2026-11-11-prerun-10

**Pre-run 10 of the Wednesday neuron.** The neuron stays [tn10-storm-2026-11-11](https://github.com/STP-KAS/tn10-storm-2026-11-11). This repo does not edit that repo, does not write `REVIEW_CLOSED`, and does not set or move a clock for it. [tn10-storm-2026-11-10](https://github.com/STP-KAS/tn10-storm-2026-11-10) (Tuesday) is not edited from here either.

> **Our own testing.** This is our own Kaspa Testnet-10 testing, run on our own machines and nodes. What these pages report is what we observed in this run; it is not a claim of how TN10 or Kaspa behave in general.

**Where this starts.** Pre-runs 1 to 4 failed and are closed. Pre-runs 5 to 9 finished through RETURN and are closed. The index of all of them is the [pre-run 2 README](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-2#pre-runs-in-this-rehearsal). This repo starts from [pre-run 9's locks/LOCKED.md](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-9/blob/485e418/locks/LOCKED.md) at commit 485e418, copied here as [locks/LOCKED.md](locks/LOCKED.md), with a pre-run 10 section added at the end.

## What pre-run 9 left open

In [pre-run 9](https://github.com/STP-KAS/tn10-storm-2026-11-11-prerun-9) we observed blocks taking about 120,000–130,000 transactions a minute when pushed. At 1,800 tx/s our payments were included as sent, but the chained low-fee covenant families had already slowed: floor (100) at about 13 percent of its HOLD-1 hop rate, double (200) 25 percent, triple (300) 38 percent, high (1000) 92 percent. Pre-run 9 had no step between 1,013 and 1,800, so it could not say where that slowdown starts. Its Mini second read also counted every hop twice.

## What pre-run 10 tries

The question: where do cheap covenant chains start to slow, comparing payment load at 1,500 tx/s and 1,800 tx/s?

- **Two measured steps, nothing over capacity.** HOLD-1 1,013 tx/s (baseline), HOLD-2 1,500 (about 70–80 percent of the block space we observed), HOLD-3 1,800 (pre-run 9's HOLD-2, repeated for comparison). The rate drops to 1,013 as soon as HOLD-3 is scored; the HOLD-4 minute is an observation at 1,013, and RETURN is 1,013. Pre-run 9's 2,500 step is dropped: in pre-run 8 our over-capacity load crowded out other TN10 users, and we do not need that again for this question.
- **Cohorts kept from pre-run 9, so the runs compare.** Floor (families 1–4) 100 sompi/gram, double (5–7) 200, triple (8–10) 300 on the desk's private node, triple-pub (11–13) 300 on the kept public kaspads, high (14–16) 1000. Payments 150. Triple and triple-pub are a single same-fee pair on two paths, so a path effect can be told apart from a fee effect; every other cohort is on one path (the desk node). Reasons in [plan/PLAN.md](plan/PLAN.md#why-this-shape).
- **The selection rule, as read for pre-run 9.** rusty-kaspa v2.1.0 takes every ready transaction while they fit in a block, and otherwise picks at random with weight (fee/mass)³; a transaction whose parent is still in the mempool is not a candidate ([plan/PLAN.md](plan/PLAN.md#selection-rule)).
- **Counting.** The desk's private node counts inclusion, per minute and per cohort (approved by the operator on 2026-11-11). Mini's second read now counts one hop per transaction (pre-run 9 counted each hop's two covenant outputs); checked offline. It is still a second read, not the inclusion figure.
- **Kept as before.** Scoring is three clean minutes of submit-OK, or `NOT MET` after one repair. MET means submit-OK, not inclusion; each step file also says in how many minutes our payments were included within 10 percent. The bot sends in HOLD-4 only if a third unique public kaspad is free, or files a legal `NO SEND`.

All locked lines from earlier pre-runs stay: no runner restart mid-run, children detached, a family stall is not dirt, a full mempool returns the coin, the repair starts missing senders and hands pools off, git retries with a local FAILED file, unique kaspads, the abort line, the desk node is never stopped.

## Machines

| Machine | Go file | First sentence |
|---|---|---|
| Desk | [GO-DESK.md](GO-DESK.md) | DESK. I send and count on pre-run 10. This is not Wednesday. |
| Mini | [GO-MINI.md](GO-MINI.md) | MINI. I count pre-run 10 as the second read. I do not send. This is not Wednesday. |
| Bot | [GO-BOT.md](GO-BOT.md) | GROKBOT. I send payments on the pre-run 10 HOLD-4 only. I do not count. This is not Wednesday. |

The operator does not paste. On 2026-11-12 at 07:51 Brussels time he said "Go" for pre-run 10; that is the arm. The agents start the runners once the gates are facts. [GO.md](GO.md) is the map, [PLAYBOOK.md](PLAYBOOK.md) has the roles and gates, and [plan/PLAN.md](plan/PLAN.md) has the targets and the reasons.

## Gates, in order

No clock. Each gate is a fact read from a node or from origin.

1. Mini's TN10 node is up from its own data, synced, DAA moving.
2. The desk's private TN10 node is up from its own data (PowerShell 7), synced, DAA moving.
3. No other runner or waiter is up. The lane is above the abort line (2,500 coins, 18,000 usable tKAS). The desk's private candidate list is present.
4. `hashes/SIXTEEN.md` is on origin: sixteen rows and an On origin line, from the sixteen-family path.
5. The desk pushes `logs/PRE-RUN-OPEN.md`; Mini pushes `logs/MINI-ARMED.md`.
6. The desk counter is up. Then the families, then the payment steps.

## What a decent result is

- `hashes/SIXTEEN.md` on origin before the first family submit.
- HOLD-1 met.
- Every step file carries submit-OK and an inclusion count per minute, each minute marked kept pace or lagging, and hops per minute for all five cohorts.
- Hops included per minute and submit-to-landing per cohort for HOLD-2 (1,500) and HOLD-3 (1,800), with triple and triple-pub side by side, so we can say at which step the cheap tiers start to slow.
- A HOLD-4 desk file, a bot file or a legal `NO SEND`, and a Mini file.
- No id, txid, key, address, host, or port in this repo.

A miss stays in this repo. A next attempt is a new repo and starts from this repo's lock file.

**Part of [tn-master](https://github.com/STP-KAS/tn-master).** The rule is [docs/NEURON.md](https://github.com/STP-KAS/tn-master/blob/main/docs/NEURON.md). This pre-run is its own row. It is not row 47.
