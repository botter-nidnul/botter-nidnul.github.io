Available from [my Urbit github fork](https://github.com/botter-nidnul/urbit/releases/tag/urbit-v0.10.4-aarch64).

If you use these on Raspbian you will still have to follow *Step One: Kernel* from [Steps to Urbit on Raspberry Pi](Steps_to_Urbit_on_Raspberry_Pi.md) but the rest of that guide can be ignored.

```
curl -OL https://github.com/botter-nidnul/urbit/releases/download/urbit-v0.10.4-aarch64/urbit-v0.10.4-linux-arm64.tgz
tar xzf urbit-v0.10.4-linux-arm64.tgz
cd ce095f1d381cdd12af4f09e5d7ab0c64c352ddf3-linux-arm64
./urbit
```

This fork has stripped out the making of release binaries for x86_64 and MacOS, and running `make release` will only build for aarch64. It uses an updated set of [nixcrpkgs](https://github.com/pololu/nixcrpkgs). The version of musl was increased to the latest in order to get these static binaries to work on aarch64. The openssl build scripts were also modified to get openssl to build inside the nix sandbox that has been enabled by default in recent nix releases.
