# Artifact provenance

All artifacts come from the Bluefox Aura A1 stock release
`BLUEFOX_J583_A8_Aura_A1_EN_V1.0.1_20260924_09241748`, fingerprint
`BLUEFOX/Aura_A1/Aura_A1t:16/BP2A.250605.031.A3/20260924:user/release-keys`.

## Kernel and device trees

| Artifact | Size | SHA-256 |
| --- | ---: | --- |
| Stock `boot.img` | 67,108,864 | `b54695d5ccd088203a45c9ce1f4fbc8d239d5fda7b6686681690b03f211e8834` |
| `6.12/Image.lz4` | 20,227,821 | `0bcdaf4b6136927caf69b616cec16fa65ffb02dab3bdbf8f4258ab93d60a5bf2` |
| Stock `vendor_boot.img` | 67,108,864 | `9a405b6b8acf3995b679bd28f68d36979e1cb5c776fc4faf742dec3d1dab3444` |
| `6.12/dtb/mt6789.dtb` | 192,144 | `2f1080e378a21ac3b8741dc56886036c90c63d54db4f0b4f1206584927953089` |
| Stock DTBO partition | 8,388,608 | `0660ef29c58efa77fb8773567a6e181af85a1a071bc67368f936f0eb9d643592` |
| `6.12/dtbo.img` | 37,856 | `6fa684e7ac4e402a1938ff793dc8de7880a8f107d581c3c8876794c82f334b3f` |

The kernel reports
`6.12.69-android16-6-g86dc53cfe87f-ab15464463-4k`. The repository stores the
kernel payload rather than a complete boot image. The DTBO build input excludes
the stock AVB footer so the Android build can generate the final footer once.

## Module topology

| Partition source | Modules | Normal load list | Recovery load list |
| --- | ---: | ---: | ---: |
| `system_dlkm` | 82 | 82 | — |
| `vendor_dlkm` | 188 | 169 | — |
| Vendor ramdisk | 174 | 166 | 169 |

Module binaries and their dependency metadata remain byte-for-byte in their
stock partition directories. The recovery load policy is the sole exception:
`modules.load.recovery` omits `haptic_rt6010.ko` to avoid the stock driver's
force-feedback teardown crash when recovery exits. Duplicate basenames across
partitions are distinct binaries and must not be flattened or deduplicated.

`SHA256SUMS` covers only the build artifacts below `6.12/`.
