JIT is a sysmodule for run-time code generation on development kits
(allowing for overlapping R-X and RW- views of memory). This system
module is not present in retail units.

# jit:u

This is
"nn::jitsrv::IJitService".

| Cmd | Name                 | Notes                                                       |
| --- | -------------------- | ----------------------------------------------------------- |
| 0   | CreateJitEnvironment | Returns an [\#IJitEnvironment](#IJitEnvironment "wikilink") |
|     |                      |                                                             |

# IJitEnvironment

This is "nn::jitsrv::IJitEnvironment".

| Cmd  | Name           |
| ---- | -------------- |
| 0    | Control        |
| 1    | GenerateCode   |
| 1000 | LoadPlugin     |
| 1001 | GetCodeAddress |
|      |                |
