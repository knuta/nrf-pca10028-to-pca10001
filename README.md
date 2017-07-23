# pca10028-to-pca10001
Convert a tree of build files from NRF51422 (PCA10028) to NRF51822 (PCA10001).

This converts a set of build files for a Nordic Semiconductor BLE project from
the device PCA10028 (which is supported by version 12.3.0 of the SDK) to one
supporting the device PCA10001 (which has no official examples in the SDK any
longer). After running this script on a build directory, it should build and
run for the PCA10001.

This script has been tested with nRF SDK 12.3.0 and S130 SoftDevice 2.0.1.
The RAM values may be different for other softdevices.

## What it does

In addition to all references to the board name in defines and file
names being renamed, the script also adjusts the memory sizes to
account for the NRF51822 only having 16 kB of RAM:

| Value     | PCA10028   | PCA10001   | Used by           |
|-----------|------------|------------|-------------------|
| RAM start | 0x20001870 | 0x20001fe8 | Keil, GCC and IAR |
| RAM size  |     0x6790 |     0x2018 | Keil and GCC      |
| RAM end   | 0x20007fff | 0x20003fff | IAR               |

## How to use it

Just copy the folder to a new location and run the script on the folder. The
conversion will be done in-place.

```sh
cp -r pca10028 pca10001
pca10028-to-pca10001 pca10001
```

## Dependencies

This script has the following dependencies:

 - /bin/sh
 - Perl
 - The Perl-based version of rename(1p) (the one in Debian/Ubuntu)

## License

pca10028-to-pca10001 is released under the MIT license.
