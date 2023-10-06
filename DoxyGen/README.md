# Creating the documentation

One of the advatnages of the pack concept is that you can easily incorporate additional files in the deliverable. Adding the documentation to the pack file ensures that versioned documentation resembles the software contents. The documentation in this directory is a small example using [Doxygen](https://www.doxygen.nl/) which is widely used in source code documentation. Other mechanisms/tools might be used as well, as long as they produce HTML output which is the recommended form.

## Contents

This is the strucutre of this documentation example.

| File/folder | Purpose |
|-------------|---------|
| [`Doxygen_Templates`](./Doxygen_Templates/) | Files that are used to create the look and feel of the documentation. Taylor to your needs. |
| [`src`](./src/) | The documentation source files. |
| [`src/images`](./src/images/) | Images used in the documentation. |
| [`check_links.sh`](./check_links.sh) | Script for checking the documentation links for consistency and availability. |
| [`gen_doc.sh`](./gen_doc.sh) | Documentation generation script. |
| [`myswcomp.dxy.in`](./myswcomp.dxy.in) | Source file that is used to generate the Doxygen control file [`myswcomp.dxy`](./myswcomp.dxy) based on the current status of the software component. |

## Documentation flow

1. Adjiust the files in the [`Doxygen_Templates`](./Doxygen_Templates/)-directory to your needs.
1. Create the documentation using the source files and annotated code (refer to the [Doxygen documentation](https://www.doxygen.nl/manual/index.html) on how to do that).
1. Generate the documentation using the [`gen_doc.sh`](./gen_doc.sh) script.
1. The generated documentation will be created in `../Documentation`. This is also the directory that is used in the `gen_pack.sh` script to be shipped with the CMSIS-Pack. The `Doxygen` source folder will not be inlcuded in the final deliverables.