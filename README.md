# Overview

This is a quick and dirty Dlang wrapper around keccak-tiny (a sha3 implementation written in C).  Improve it, fix it, use it, and eventually a hero will offer to maintain it, make it into a proper Dlang module.

From NIST: NIST announced the SHA-3 Cryptographic Hash Algorithm Competition on November 2, 2007, and ended the competition on October 2, 2012, when it announced KECCAK as the winning algorithm to be standardized as the new SHA-3.

## References

- NIST SHA-3 Project https://csrc.nist.gov/projects/hash-functions/sha-3-project
- Wrapper around: https://github.com/IoTone/keccak-tiny (fork of) https://github.com/RomanHuryk/keccak-tiny forked from: https://github.com/coruus/keccak-tiny (not maintained)
- Reading on @safe and @trusted: https://dlang.org/blog/2016/09/28/how-to-write-trusted-code-in-d/
- Test cases inspired by: https://github.com/emn178/js-sha3#example

## Building

Because this D module wraps a C library, you the reader will need to build the library through means available on your platform.  It appears the keecak-tiny library will build with clang, gcc, or probably some other variant not mentioned.

From a posix compliant shell, run sh setup-deps.sh to grab and build keccak-tiny.  

### Windows Notes

Since we don't provide a VS build or a fancy cmake build (that might be a good idea in the future), it is recommended that you use a POSIX shell like a ConEMU or similar to build.  This implies that you will have a Clang or gcc installed as well.  Install it before you get started.

On windows you may need to rename your library to keccak-tiny.lib.

### Building the D library

We recommend a Dlang compiler based on DMD v2.076.1 or later.

dub build --compiler=ldc2

## Testing

dub test --compiler=ldc2

## Examples


```
import iotone.libkeccak

ubyte[32] dataout;
ubyte[] datain = cast(ubyte[])("The quick brown fox jumps over the lazy dog".dup);
ubyte[] datain2 = cast(ubyte[])("".dup);
shake256(dataout.ptr, 32 /* bytes */, datain.ptr, datain.length);

```
