# clone-lin-maker-vat-fork

Experimental **LIN** clone of MakerDAO / Sky `Vat.fork` — the Dai and USDS
CDP-split kernel (signed `_sub`/`_add` of `ink`/`art` on two urns, then both
sides must stay safe and non-dusty, with dual `wish` consent).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [makerdao/dss](https://github.com/makerdao/dss) `fa4f6630afb0624d04a003e920b0d71a00331d98`
  - `src/vat.sol` sha256 `9016fd94f0f1b014abf184edab86a3f5843042b17e3734407e0f0fabb920f49f` blob `ff90bbed5b36e54318bd5461cbf32e4167df2b28`
  - License AGPL-3.0-or-later. This repository does **not** vendor the Solidity source.
- **LIN kernel:** [`src/lin_maker_vat_fork.lin`](src/lin_maker_vat_fork.lin) (identical to lin-open)
- **C11 oracle copy:** [`test/oracles/maker_vat_fork_c11.c`](test/oracles/maker_vat_fork_c11.c)
- **Proofs (lin-open only):** `examples/maker_vat_fork/` and `make maker-vat-fork-proof`
- **Class:** EXPERIMENTAL uint64-scale, `RAY' = 1e9`. Not mainnet `RAY=1e27`. Not wad×ray tab. Not a production vat replacement.

Named goldens: SAFE_SPLIT `dink=1e9 dart=5e8` on `u=5e9/2e9 v=3e9/1e9` rate=spot=1e9 dust=1e18 wish=1,1 → **fork_ok=1**, both vaults `4e9/1.5e9`;
UNSAFE_DST thin collateral → **0**; leftover tab below dust → **0**; no-wish → **0**;
signed negative dink moves ink dst→src; ink and art conserved; no `live`, no `wards` (wish only);
naive i64 `7e18*3e18` wraps; 128-bit muldiv fail-closes to **0**.

## Reproduce proofs (in lin-open)

```bash
make maker-vat-fork-proof
# or: python3 test/prove_maker_vat_fork_external.py
```

## Not claimed

Uint256 / RAY=1e27 / wad×ray tab mainnet parity.
LIN replacing Maker, Sky, vat, or the EVM. TVL or dollar savings. zk soundness.
`wish` mappings as hidden storage. `vat.frob` (see clone-lin-maker-vat-frob). `vat.grab` (see clone-lin-maker-vat-grab). `vat.suck` (see clone-lin-maker-vat-suck).
