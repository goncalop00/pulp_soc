# Dissertation fork — SoC-level fixes for SE bring-up (pulp_soc)

Fork of [`pulp-platform/pulp_soc`](https://github.com/pulp-platform/pulp_soc)
with two SoC-level fixes needed for the Streaming Engine evaluation, for the
MSc dissertation *Configurable Streaming Engine for RISC-V Systems* (Gonçalo
Pereira, FEUP).

## `clusterv2` branch

On top of the upstream `clusterv2` tag:

- `rtl/fc/fc_subsystem.sv` — ties the Fabric Controller's stream-instruction
  ports to non-blocking constants (the FC has no SE attached)
- `rtl/pulp_soc/pulp_soc.sv` — fixes a `SELECTABLE_HARTS` overflow that
  dropped the FC hart bit, leaving the FC marked unavailable

Both are detailed in the dissertation's implementation chapter.

## Where it sits

Cloned into `ips/pulp_soc/` by the top-level
[`pulp_streaming_engine`](https://github.com/goncalop00/pulp_streaming_engine)
fork. The `upstream` remote is kept, so
`git diff upstream/clusterv2..origin/clusterv2` shows the full delta.

## License

Solderpad Hardware License v0.51 (inherited from upstream).
