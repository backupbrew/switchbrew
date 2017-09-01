This is the 1000000000000001 title used at
[factory](Factory%20Setup.md "wikilink"). Process-name is
"SystemInitializ", internally in strings it's referred to as
"SystemInitializer". The usage strings (see below) refer to it as
"SystemUpdater", which might be an old name since that's the only
reference to it.

Initial system installer: used to write/verify console specific
*calibration* data such as asymmetric keys and write/verify NAND
partitions from an initial installation image. Hence, this initializes
the entire NAND. This includes an option for erasing NAND.

Uses input arguments from <argc/argv>. Returns without doing anything if
the required arguments are not passed. Uses logging code for all text
output which basically uses [svcOutputDebugString](SVC.md "wikilink")
eventually.

This is a "TargetTool": multiple path strings contain "TargetTools"(.nss
string / source path strings).

This is basically a cmd-line tool.

Output from all svcOutputDebugString calls combined, with no arguments
passed:

` [ERROR] Argument(-i | --input) is not found.`  
` `  
` SystemUpdater: Update the system by the system initial image.`  
` `  
` Usage: SystemUpdater -i `<arg>` | --input `<arg>` [--dry-run] [--print-info] [--enable-overwriting-production-info] [--enable-erase-emmc] -r `<arg>` | --output-request `<arg>` -s `<arg>` | --input-response `<arg>` -o `<arg>` | --output-result `<arg>` [--verify-key] [--cal-image `<arg>`] [-s | --silent] [-v | --verbose] [--debug] [-h |--help]`  
` `  
` Arguments:`  
`     -i `<arg>` | --input `<arg>`  Input the initial image.`  
`     --dry-run Run without writing to the storage.`  
`   `  
`   --print-info    Print about the initial image.`  
`     --enable-overwriting-production-info  For device production.`  
`     --enable-erase-emmc   For device production.`  
`     -r `<arg>` | --output-request `<arg>` set request path as output.`  
`     -s `<arg>` | --input-response `<arg>` set response path as input.`  
`     -o `<arg>` | --output-result `<arg>`  set result path as output.`  
`     --verify-key  verify key pairs in cal.`  
`     --cal-image `<arg>` set cal image path.`  
`     -s | --silent Disable logs except errors.`  
`     -v | --verbose    Output many logs.`  
`     --debug   Output many logs for developer.`  
`     -h | --help   Display help.`
