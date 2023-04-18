# Software Pack Hands-On Example

This repository contains a simple software pack hands-on example. It is created by the imaginary "ACME Corp." and
contains bundles for an *evaluation* and a *commercial* version of a software component that is available in two flavors:
*debug* and *release*. 

>NOTE: *evaluation* and *commercial* are typically two different packs, but this first hands-on is simple.

Content                        | Description
:------------------------------|----------------------------------------
[`gen_pack.sh`](./gen_pack.sh) | Script that builds the pack; refer to [usage information](https://github.com/Open-CMSIS-Pack/gen-pack#get-started) for configuration details.
[`.github/workflows/pack.yaml`](./.github/workflows/pack.yaml)  | GitHub workflow that generates the pack on every commit.
