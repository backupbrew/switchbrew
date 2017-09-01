This is the 1000000000000001 title used at
[factory](Factory%20Setup.md "wikilink"). Process-name is
"SystemInitializ", internally in strings it's referred to as
"SystemInitializer".

Initial system installer: used to write/verify console specific
*calibration* data such as asymmetric keys and write/verify NAND
partitions from an initial installation image. Hence, this initializes
the entire NAND. This includes an option for erasing NAND.

Uses input parameters from <argc/argv>. Returns without doing anything
if the required parameters are not passed. Uses logging code for all
text output which basically uses svcOutputDebugString eventually.
