> **Experimental. We are just trying this.** [Disclaimer](DISCLAIMER.md) · Kaspa Testnet-10 only; tKAS has no value.
>
> **This is the playbook for pre-run 10.** It is not Wednesday. It is not Tuesday. It is not pre-run 1, 2, 3, 4, 5, 6, 7, 8, or 9. It does not start a machine and it does not arm one.

# Playbook

Who does what, and the gates before each machine may start. The plan is [plan/PLAN.md](plan/PLAN.md), the locks are [locks/LOCKED.md](locks/LOCKED.md), and the go files are the three GO pages. This page does not override them.

## Oversight

TN10 ops oversees this rehearsal end to end: Mini, the desk (Build), and the bot. TN10 only. Never mainnet. Do not edit the Tuesday repo, the Wednesday repo, or pre-run 1's to 9's go files. Do not write `REVIEW_CLOSED`.

For pre-run 10 the operator does not paste. On 2026-11-12 at 07:51 Brussels time he said "Go" for pre-run 10 (spending TN10 wallet funds as needed is approved). That is the arm. The agents start their runners once the gates are facts.

## Start gates

1. **Mini node synced.** Existing TN10 kaspad, existing data, no wipe. `isSynced` true, DAA moving.
2. **Desk node synced.** Existing private TN10 kaspad, existing data, loopback only, started with `pwsh`. No wipe. Synced, DAA moving.
3. **No other runner.** No earlier runner, waiter, or counter on any machine. Lane above the abort line. The desk's private candidate list is present and not empty (`HELD candidates-missing` otherwise).
4. **Hashes.** `hashes/SIXTEEN.md` with sixteen rows and an On origin line, from [tools/sixteen](tools/sixteen/README.md).
5. **Open.** The desk pushes `logs/PRE-RUN-OPEN.md`. Mini then pushes `logs/MINI-ARMED.md`.
6. **Counter, families, senders.** The desk runner starts the counter on its private node and waits for its start line (`HELD counter-down` otherwise). Then the genesis from the bundle that wrote `hashes/SIXTEEN.md`, the families, and the payment steps.

## Who does what

| Who | Role | What not to do |
|---|---|---|
| **Desk (Build)** | Sends the sixteen families (five cohorts: four fees, and one fee on two paths) and the payment offers. Its private TN10 node counts what the chain accepted (lock line (iv)). Publishes `hashes/SIXTEEN.md`, `logs/PRE-RUN-OPEN.md`, `counts/desk/` per step, `counts/chain/TIMELINE.md` after the tail, and `logs/METHOD.md`. | Do not stop or wipe the desk node. No Windows PowerShell 5.1, no `KaspaPublicNode`, no devnet. No 8- or 32-family publisher. No second runner. Never restart the runner mid-run. |
| **Mini** | Second chain read on its own node. Does not send, mine, or hold a key. Publishes `logs/MINI-ARMED.md`, then `counts/mini/` when the matching desk file is on origin. Each head is Mini's own read: `READ`, `PARTIAL`, or `NOT READ`. | Do not wipe. Do not repeat the desk's head as Mini's. |
| **Bot (TN10 ops)** | Sends payments in the HOLD-4 minute only, on a synced public kaspad that is not one the desk kept, or publishes a legal `NO SEND`. | Do not send on HOLD-1, HOLD-2, HOLD-3, or RETURN. One waiter. No local node. |

## Status when this repo was opened

Not a gate. A status line, so nobody guesses. Read on 2026-11-12 between 06:52Z and 07:05Z. This is our own TN10 testing; status lines are what we read on our own machines.

- Mini: existing TN10 kaspad 2.1.0 up since 2026-11-11, no wipe; its sync is read and logged by its runner before `MINI-ARMED`. Pre-run 9's Mini runner ended at 2026-11-12T01:48:42Z.
- Desk: existing private TN10 kaspad 2.1.0 up with `pwsh` since 2026-11-11, no wipe, synced, DAA moving. It is not stopped for this pre-run. No pre-run 9 runner or child is running.
- Box: no local TN10 node. No bot waiter running.
- Lane and pile: lane 5,541 coins and 245,475 usable tKAS before funding, above the abort line. The payment key holds 8,400 coins. Keys 1–15 got a fresh genesis coin from the lane on 2026-11-12 at 06:56:53Z (15 transactions, none rejected; amounts and transaction ids are kept in the operator's private notes, not here).
- Known risks, not fixed mid-run:
  - Triple-pub's funding coins are still read from the desk node; a public node may briefly refuse a coin it has not yet seen spent. Such rejects are logged.
  - 1,800 tx/s sat at the edge of the block space we observed in pre-runs 8 and 9. If other TN10 users add load, HOLD-3 may go briefly over capacity; the rate still drops to 1,013 as soon as HOLD-3 is scored.
  - Each family is a chain of hops, so a hop waits for its parent whatever its fee (see [plan/PLAN.md](plan/PLAN.md#selection-rule)).
  - The run sees no miner's template; what a public kaspad's own template would pick is inferred, not read.
  - Only two unique public kaspads answered in every check so far, and the desk keeps both, so the bot is expected to file `NO SEND no-free-node`.

## Offline rehearsal, recorded before `PRE-RUN-OPEN`

Rehearsal A (p10-a), 2026-11-12 06:58:06Z to 07:20:59Z (desk, Brussels 07:58 to 08:21). The real pre-run 10 desk runner, counter, payment sender and the rehearsal family sender ran against pre-run 9's stand-in node on the desk, with a local bare origin. The stand-in accepted at most about 2,000 transactions a second on chain (so HOLD-2 at 1,500 and HOLD-3 at 1,800 were both under it), carried other traffic, let the desk view fall behind for 100 s inside HOLD-2, and was set to replace one chain block after 420 s. Nothing was sent to the network. Short times: 2-minute tail.

- Preflight kept two unique kaspads (one candidate was the same kaspad as another). `FAMILY_PUBLIC_MAP 11:public-1,12:public-5,13:public-1`. `FEE_SPLIT` and every submit row's rate and path were checked: floor 100, double 200, triple 300 and high 1000 on the desk node, triple-pub 300 on the public nodes. 16 families attempting. Pile 8,400 dealt 1,400 to each of six senders.
- HOLD-1 `MET` (60,753 / 60,773 / 60,882 submit-OK). HOLD-2 at 1,500 `MET` (90,157 / 89,700 / 90,116 submit-OK, included within 10 percent in 3 of 3 minutes); all three minutes marked `LAGGING` because of the planned desk-view lag, and the file said so. HOLD-3 at 1,800 `MET` (107,841 / 108,170 / 108,263; included 108,153 / 107,723 / 108,393, kept pace).
- The rate fell to 1,013 at 07:10:12Z as HOLD-3 was scored (`MEASURED_END`). HOLD-4 pinned 07:14Z and ran at 1,013 (`OBSERVATION`, 60,891 submit-OK). RETURN `MET` (60,739 / 60,642 / 60,923). The runner published `counts/chain/TIMELINE.md` and `logs/METHOD.md` (with the "our own TN10 testing" line) and exited 0. No rehearsal process was left running.
- What the rehearsal did not exercise: the counter logged no `REORG` line, as in pre-runs 8 and 9's rehearsals; the removal path is unchanged. The stand-in lands hops by its own rule, so its cohort numbers are not a network result. Mini's classify fix was checked by its own offline tests (on the box and on Mini), not in this rehearsal.

## When something breaks

Append a worked fix to [locks/LOCKED.md](locks/LOCKED.md) in the form that page shows, and a repair line to `logs/FIXES.md`. If the run dies before RETURN, write `logs/FAILED.md`, stop every runner, waiter, and counter, and do not resume. The next attempt is a new repo that starts from this repo's lock file.
