# Third-party material

IBM, Dell, ADIC and Quantum firmware/update executables retain their original
copyrights and embedded notices. This project is not affiliated with those
vendors and does not provide the original proprietary source tree or a blanket
open-source license for their binaries.

The XA disassembler includes MAME-derived material under its supplied
BSD-3-Clause terms. See
`src/library-q3/tools/xa-disassembler/LICENSE` and notices in `xadasm.cpp` and
`xadasm.h`. The standalone driver/shim is included for offline instruction
inspection.

Optional analysis dependencies (Unicorn, Capstone, Keystone, Pillow, Playwright,
Zig and Terser) are not bundled. Their own distributions provide their licenses.
The compiled RMU patch ELF and its source/hash record are included for exact
reproduction; no vendor application source is represented as newly compiled.

## Original input provenance

- IBM 3582 314B.GY001 and IBM 210C.00002: supplied IBM firmware preserved in
  the project checkpoint; originals included for rollback/rebuild.
- Dell library 310D.GY004 and `dls24.exe`: Dell A13 package,
  `DELL_POWERVAULT-132T-TAPE-LI_A13_R222331.exe`.
  Original download: https://dl.dell.com/tape-dev/DELL_POWERVAULT-132T-TAPE-LI_A13_R222331.exe
- ADIC/Quantum library 313A.GY003: recovered Scalar24 LTO4 package
  `Scalar24_LTO-4_v313.zip`, previously acquired and verified in the project.
  Vendor support: https://www.quantum.com/en/service-support/downloads-and-firmware/
- MAME XA decoder upstream:
  https://github.com/mamedev/mame/tree/master/src/devices/cpu/xa
- LTO compatibility reference:
  https://www.lto.org/lto-generation-compatibility/

`MANIFEST.json` and `SHA256SUMS.txt` identify the actual included bytes. Historical
source URLs are provenance, not a claim that old public downloads remain live.
