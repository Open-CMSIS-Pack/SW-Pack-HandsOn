# Software Pack Hands-On Example

This repository contains a simple software pack hands-on example. It is created by the imaginary "ACME Corp." and
contains bundles for an *evaluation* and a *commercial* version of a software component that is available in two flavors:
*debug* and *release*. 

>NOTE: *evaluation* and *commercial* are typically two different packs, but this first hands-on is simple.

Content                        | Description
:------------------------------|----------------------------------------
[`gen_pack.sh`](./gen_pack.sh) | Script that builds the pack; refer to [usage information](https://github.com/Open-CMSIS-Pack/gen-pack#get-started) for configuration details.
[`.github/workflows/pack.yaml`](./.github/workflows/pack.yaml)  | GitHub workflow that generates the pack on every commit.

## Pack Development

### Tool-Environment (Recommended)

- MDK v5.38 with default installation path (C:\Keil_v5\)
- [CMSIS-Toolbox v1.6.0](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/releases) or higher (update files in C:\Keil_v5\ARM\ctools)
- [VS Code](https://code.visualstudio.com/) with [XML Language Support by Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml)

> NOTE: With CMSIS-Toolbox v1.5.0 the XML schema check needs to be done manually

### Local Pack Development

1. Clone this repository
2. Register this pack with `cpackget` via [PDSC file](https://github.com/Open-CMSIS-Pack/cpackget/blob/main/README.md#adding-packs) these commands:

   ```txt
   > cpackget update-index                    // optional to ensure that pack index is up-to-date
   > cpackget add ACME.ACME_Middleware.pdsc   // pack now appears in toolchains, i.e. in MDK
   > csolution list packs
   ```

For changing the XML it is recommended to use VS Code. After modifications to the `*.pdsc` file run:

```txt
> packchk ACME.ACME_Middleware.pdsc -i %LocalAppData%/Arm/Packs/ARM/CMSIS/5.9.0/ARM.CMSIS.pdsc -s /Keil_v5/UV4/PACK.xsd
```

The pack can be created locally in the directory `output` using a bash console:

```txt
$ ./gen_pack.sh -V
```

### Pack Creation on GitHub

Once changes are committed the [GitHub Action](https://github.com/Open-CMSIS-Pack/SW-Pack-HandsOn/actions) creates the pack.

### Publish Pack

The pack can be hosted on the [\<url\>](https://github.com/Open-CMSIS-Pack/SW-Pack-HandsOn/blob/main/ACME.ACME_Middleware.pdsc#L8) specified in the `*.pdsc` file.

Refer to [Publish a Pack](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/createPackPublish.html) in the Open-CMSIS-Pack specification for further details.