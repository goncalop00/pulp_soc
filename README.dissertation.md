# Dissertation fork — SoC-level fixes for Streaming Engine bring-up

A fork of [`pulp-platform/pulp_soc`](https://github.com/pulp-platform/pulp_soc)
carrying two SoC-level fixes needed for the Streaming Engine evaluation in
the master's dissertation:

> **Configurable Streaming Engine for RISC-V Systems**
> Gonçalo Pereira — Faculdade de Engenharia da Universidade do Porto (FEUP)

The upstream `README.md` is preserved alongside this file.

## The `clusterv2` branch

On top of the upstream `clusterv2` tag, this fork adds:

- `rtl/fc/fc_subsystem.sv` — ties the Fabric Controller's RI5CY
  stream-instruction ports to non-blocking constants, since the FC has no
  Streaming Engine attached.
- `rtl/pulp_soc/pulp_soc.sv` — fixes a `SELECTABLE_HARTS` overflow that was
  silently dropping the FC hart bit, leaving the FC marked unavailable.

Both fixes are detailed in the dissertation's implementation chapter.

## Where it sits

Cloned into `ips/pulp_soc/` by the top-level
[`pulp_streaming_engine`](https://github.com/goncalop00/pulp_streaming_engine)
fork through its `ips_list.yml` manifest. The `upstream` Git remote is
preserved, so `git diff upstream/clusterv2..origin/clusterv2` shows the
complete delta.

## License

Inherits the Solderpad Hardware License v0.51 from the upstream repository.