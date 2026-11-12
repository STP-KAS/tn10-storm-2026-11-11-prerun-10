> **Experimental. We are just trying this.** [Disclaimer](../../DISCLAIMER.md) · Kaspa Testnet-10 only. No key, id, address, host, or port in these files.

# Mini's second read, pre-run 10

- `mini-runner.mjs`: pre-run 9's Mini counter, pointed at this repo and the pre-run 10 offers. Changed for pre-run 10: `classify()` gives one row per transaction, not one per covenant output. A hop transaction carries two covenant outputs, so pre-run 9's Mini counted every hop twice (its hop columns were exactly twice the desk's in 12 of 13 scored-minute rows; the 13th was one hop off). Both outputs are still remembered as possible parents, so the next hop is still recognised whichever output it spends. Kept from pre-run 9: each accepted transaction id counts once (`mini-dedupe.mjs`), and a removed chain block takes its transactions back out of a minute that is still open.
- `mini-classify-test.mjs`: offline check of the fix. It lifts `classify()` out of the runner and feeds it a genesis, hops with two covenant outputs (spending either output), a hop with two different covenant ids, a payment and an unknown id; a 100-hop chain must give 100 hop rows. It passed on the box before the run.
- `mini-dedupe-test.mjs`, `mini-dedupe.mjs`: pre-run 9's dedupe and its offline check, unchanged; passed again before the run.

This is meant to make Mini's second read comparable to the desk's, not to replace the desk counter, which stays the inclusion figure.
