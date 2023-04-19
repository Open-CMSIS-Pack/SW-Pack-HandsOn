# Create a Software Pack - Hands-On Example

This repository explains the steps to create a simple software pack using the Open-CMSIS-Pack technology. 

The pack contains software from the imaginary "ACME Corp." and shows how to frame a middelware as *evaluation* and *commercial* version.
The software component itself is available in two flavors: *debug* (that could have additional test outputs) and *release*.

>NOTE: *evaluation* and *commercial* are typically two different packs, but this first hands-on is simple and uses just one pack for it.

Content                        | Description
:------------------------------|----------------------------------------
[`gen_pack.sh`](./gen_pack.sh) | Script that builds the pack; refer to [usage information](https://github.com/Open-CMSIS-Pack/gen-pack#get-started) for configuration details.
[`.github/workflows/pack.yaml`](./.github/workflows/pack.yaml)  | GitHub workflow that generates the pack on every commit.

## Benefits of Software Pack Delivery

The CMSIS-Pack technology is available in multiple toolchains. Below is a brief history:

- **2008:** CMSIS-Core has been introduced and [CMSIS](https://arm.com/cmsis) has been since then continuously extended.
- **2012:** CMSIS-Pack has been started to simplify Product Lifecycle Management (PLM) of Keil MDK and improve overall user experience.
- **2014:** CMSIS-Pack is part of Keil MDK for device support, middleware which resulted in higher adoption and lower support.
- **2017:** Eclipse version of the CMSIS-Pack system is integrated in Arm DS and IAR toolchains. Sharing packs across toolchains is now possible.
- **2020:** Discussions with ST and NXP resulted in the [Open-CMSIS-Pack](https://github.com/Open-CMSIS-Pack/) project and the [VS Code](https://marketplace.visualstudio.com/items?itemName=Arm.keil-studio-pack) integration.

### Benefits for a Software Vendor

- **Connection to users:** as software vendor you control distribution to multiple tools and web portals. For the [Arm pack system](https://www.keil.arm.com/packs/) new releases are scanned once per day, making it available to the entire user based. Documentation links in the software pack lets you connect with your users.

- **Support business goals:** distribute different software variants (eval, lite, full) enables users to seamlessly transition to a commercial offering.

- **One way to distribute:** for all relevant toolchains as CMSIS supports Arm Compiler, GCC, and IAR. Software scales to many devices when APIs are applied.

- **Reduces support efforts:** as it is easier for users to integrate software in projects. Product Lifecycle Management simplifies updates and notifies users about outdated configuration files.

To learn more review the session about [Generating CMSIS-Packs for Middleware](https://linaro.atlassian.net/wiki/spaces/CMSIS/pages/28897214510/Open-CMSIS-Pack+Technical+Meeting+2023-04-18#Arm-Presentation%3A-Generating-CMSIS-Packs-for-Middleware).

## Pack Development

The following section explains how to create a pack.

### Tool-Environment (Recommended)

- MDK v5.38 with default installation path (C:\Keil_v5\)
- [CMSIS-Toolbox v1.5.0](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/releases) or higher (update files in C:\Keil_v5\ARM\ctools)
- [VS Code](https://code.visualstudio.com/) with [XML Language Support by Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml)

### Steps to Create a Software Pack

- **Structure your software**
  - What are the functional blocks, are these usable separately? If so, consider separate components.
  - What are the interfaces to the device and/or hardware? 
  - Are there existing interfaces in CMSIS? Take a look to CMSIS-Drivers and consider to provide feedback.
  - If not, consider to create an API to separate device from functional parts.
  - You may provide device-specific interfaces as part of your pack but consider a separate pack as the interface could be overwritten or extended with other packs.
- **Organize and create the file list** that will be delivered as Pack
  - Each component can have source code, header and library files, documentation; separate the content logically.
- **Create the [PDSC file](ACME.ACME_Middleware.pdsc)** using your favorite editor (we recommend VS Code with XML extension).
- **Validate the software pack** using the `packchk` tool.
- **Create the software pack** using the `gen_pack` library.

### Local Pack Development

1. Clone this repository (as it serves as a getting started example)
2. Register this pack with `cpackget` via [PDSC file](https://github.com/Open-CMSIS-Pack/cpackget/blob/main/README.md#adding-packs) using this commands:

   ```txt
   cpackget update-index                    // optional to ensure that pack index is up-to-date
   cpackget add ACME.ACME_Middleware.pdsc   // pack now appears in toolchains, i.e. in MDK
   csolution list packs
   ```

For changing the [PDSC file](ACME.ACME_Middleware.pdsc) it is recommended to use VS Code with XML extension, but any editor would work.

After modifications to the [PDSC file](ACME.ACME_Middleware.pdsc) run `packchk`; include all packs that are required by your software in the validation:

Using **Command Prompt**:

```txt
packchk ACME.ACME_Middleware.pdsc -i %CMSIS_PACK_ROOT%/ARM/CMSIS/5.9.0/ARM.CMSIS.pdsc
```

Using  **Git Bash** console:

```txt
packchk ACME.ACME_Middleware.pdsc -i $CMSIS_PACK_ROOT/ARM/CMSIS/5.9.0/ARM.CMSIS.pdsc
```

With CMSIS-Toolbox v1.7.0 the XML schema check is available with packchk, the command may be then extended to:

```txt
packchk ACME.ACME_Middleware.pdsc -i $CMSIS_PACK_ROOT/ARM/CMSIS/5.9.0/ARM.CMSIS.pdsc -s /c/Keil_v5/UV4/PACK.xsd
```

The pack can be created locally in the directory `output` using **Git Bash**:

```txt
./gen_pack.sh -v
```

### Pack Creation on GitHub

Once changes are committed the [GitHub Action](https://github.com/Open-CMSIS-Pack/SW-Pack-HandsOn/actions) creates the pack.

### Publish Pack

The pack can be hosted on the [\<url\>](https://github.com/Open-CMSIS-Pack/SW-Pack-HandsOn/blob/main/ACME.ACME_Middleware.pdsc#L8) specified in the `*.pdsc` file.

Refer to [Publish a Pack](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/createPackPublish.html) in the Open-CMSIS-Pack specification for further details.

### Issues and Questions

Use [Issues](https://github.com/Open-CMSIS-Pack/SW-Pack-HandsOn/issues) on this GitHub to raise questions or submit problems.

**Happy Packing!**
