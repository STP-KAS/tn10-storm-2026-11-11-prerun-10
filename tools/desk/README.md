> **Experimental. We are just trying this.** [Disclaimer](../../DISCLAIMER.md) · Kaspa Testnet-10 only. No key, id, address, host, or port in these files.

# Desk runner, pre-run 10

Pre-run 9's runner, counter and senders, with one pre-run 10 change (lock line (x) in [locks/LOCKED.md](../../locks/LOCKED.md)).

- `desk-runner.mjs`: offers HOLD-1 1,013, HOLD-2 1,500, HOLD-3 1,800 (the two measured steps), then the rate drops to 1,013 as soon as HOLD-3 is scored; HOLD-4 and RETURN at 1,013. Everything else is pre-run 9's: five cohorts (floor 1–4 at 100, double 5–7 at 200, triple 8–10 at 300, triple-pub 11–13 at 300 on the public path, high 14–16 at 1000), `FEE_SPLIT` and `FAMILY_PATH` checks, `HELD candidates-missing` if the private candidate list is absent or empty, per-cohort columns, inclusion within 10 percent reported under each head. The method file opens with a line saying this is our own TN10 testing.
- `counter.mjs`, `pay2.mjs`, `paypool.mjs`, `preflight.mjs`: pre-run 9's, unchanged.

The family sender is kit19, unchanged from pre-run 9; it stays on the desk ([tools/sixteen/kit19-public-path.patch](../sixteen/kit19-public-path.patch)).

Everything earlier runners did stays: one runner, detached children, unique kaspads, three senders per kaspad, the fair deal and the handoff repair, git retries with a local FAILED file, never restarted mid-run.
