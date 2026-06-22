# Dissertation fork — SoC-level fixes for Streaming Engine bring-up

This fork of [`pulp-platform/pulp_soc`](https://github.com/pulp-platform/pulp_soc)
carries two SoC-level fixes required for the Streaming Engine evaluation in
the master's dissertation:

> **Configurable Streaming Engine for RISC-V Systems**
> Gonçalo Pereira — Faculdade de Engenharia da Universidade do Porto (FEUP)

The upstream `README.md` is preserved alongside this file.

## Dissertation branch

Work branch: **`clusterv2`** (same name as upstream).

It adds, on top of the upstream `clusterv2` tag:

- `rtl/fc/fc_subsystem.sv` — ties the Fabric Controller's RI5CY stream-instruction
  ports to non-blocking constants. The FC has no Streaming Engine attached;
  without this tie-off, an accidental stream instruction issued on the FC would
  hang the core waiting for a `valid`/`ready` that never arrives.
- `rtl/pulp_soc/pulp_soc.sv` — fixes a `(1 << 496)` overflow in the
  `SELECTABLE_HARTS` localparam computation. The shift was being evaluated in
  the default 32-bit width, so the bit for the FC hart (mhartid 496) was
  silently dropping to zero. The debug module then permanently marked the FC
  unavailable. Replaced with direct bit-indexing of the `NrHarts`-wide vector.

## Where it sits in the chain

Cloned into `ips/pulp_soc/` by the top-level
[`pulp_streaming_engine`](https://github.com/goncalop00/pulp_streaming_engine)
fork through its `ips_list.yml` manifest.

## Provenance

The original `pulp-platform/pulp_soc` URL is preserved as the `upstream` Git
remote. A `git diff upstream/clusterv2..origin/clusterv2` shows the complete
dissertation delta — two files, twenty-three lines.

## License

Inherits the Solderpad Hardware License v0.51 from the upstream repository.