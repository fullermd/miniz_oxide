# miniz_oxide

A pure rust replacement for the [miniz](https://github.com/richgel999/miniz) DEFLATE/zlib encoder/decoder.
The main intention of this crate is to be used as a back-end for the [flate2](https://github.com/alexcrichton/flate2-rs), but it can also be used on it's own. Using flate2 with the ```rust_backend``` feature provides an easy to use streaming API for miniz_oxide.

miniz_oxide 0.5.x Requires at least rust 1.40.0 0.3.x requires at least rust 0.36.0.

miniz_oxide features no use of unsafe code.

miniz_oxide can optionally be made to use a simd-accelerated version of adler32 via the [simd-adler32](https://crates.io/crates/simd-adler32) crate by enabling the 'simd' feature. This is not enabled by default as due to the use of simd intrinsics, the simd-adler32 has to use unsafe. The default setup uses the [adler](https://crates.io/crates/adler) crate which features no unsafe code. 

## Usage
Simple compression/decompression:
```rust

extern crate miniz_oxide;

use miniz_oxide::inflate::decompress_to_vec;
use miniz_oxide::deflate::compress_to_vec;

fn roundtrip(data: &[u8]) {
    # compress the input
    let compressed = compress_to_vec(data, 6);
    # decompress the compressed input
    let decompressed = decompress_to_vec(decompressed.as_slice()).expect("Failed to decompress!");
}

```
These simple functions will do everything in one go and are thus not recommended for use cases where the input size may be large or unknown, for that use case consider using miniz_oxide via flate2 or the low-level streaming functions instead.
