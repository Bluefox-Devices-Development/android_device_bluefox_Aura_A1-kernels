# Artifact provenance

All artifacts come from the Bluefox Aura A1 stock release
`BLUEFOX_J583_A8_Aura_A1_EN_8_128_V1.0.0_20260610`, fingerprint
`BLUEFOX/Aura_A1/Aura_A1:16/BP2A.250605.031.A3/20260610:user/release-keys`.

## Kernel and device trees

| Artifact | Size | SHA-256 |
| --- | ---: | --- |
| Stock `boot_a` partition | 67,108,864 | `d017e6df9c3e718810cb30e80dc68753b10ef97bcb0ab299d8f60a5514bfd381` |
| `6.12/Image.lz4` | 19,839,499 | `f061bde7215446a26ffdeef20840a9e33124ff297dbf126de028149f3acc0594` |
| Stock `vendor_boot.img` | 67,108,864 | `89f8ee44bf63082440f5da0bfd5909962dc4579259b485735be1efb9fd813b17` |
| `6.12/dtb/mt6789.dtb` | 191,600 | `ffb247b59b04eb8885ced9e3b61a5eb93ad7917c1876da0432655c6448e38d66` |
| Stock DTBO partition | 8,388,608 | `f133e788de051cbd3084f3686e5681b1c05f28d5335d12c9536ab9da3c71e4ad` |
| `6.12/dtbo.img` | 37,120 | `74a9b258fc88a93a7838e8ead56023cd30ed12080428025b46c66380f0b715ca` |

The kernel reports
`6.12.58-android16-6-gb0a9599c6c01-ab14987696-4k`. The repository stores the
kernel payload rather than a complete boot image. The DTBO build input excludes
the stock AVB footer so the Android build can generate the final footer once.

## Module topology

| Partition source | Modules | Normal load list | Recovery load list |
| --- | ---: | ---: | ---: |
| `system_dlkm` | 83 | 83 | — |
| `vendor_dlkm` | 188 | 169 | — |
| Vendor ramdisk | 174 | 166 | 170 |

Modules and their dependency metadata remain byte-for-byte in their stock
partition directories. Duplicate basenames across partitions are distinct
binaries and must not be flattened or deduplicated.

`SHA256SUMS` covers only the build artifacts below `6.12/`.
