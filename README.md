# bazel_sysroot_lib_amd64

This sysroot provides AMD64-specific shared libraries for Bazel builds. It is designed to be used in conjunction with the common library sysroot (`bazel_sysroot_library`) and the AMD64 LLVM toolchain sysroot (`bazel_sysroot_llvm_amd64`).

## Purpose

The `bazel_sysroot_lib_amd64` sysroot serves as the AMD64-specific library provider, containing:
- AMD64-specific shared libraries (`.so`)
- AMD64-specific static libraries (`.a`)
- Architecture-specific system dependencies

## Directory Structure

```
sysroot/
├── lib/         # AMD64-specific libraries
└── BUILD.sysroot.bazel
```

## BUILD.sysroot.bazel

The BUILD file exposes the following targets:

1. **Filegroups**:
   - `:all` - Includes the `:lib` filegroup
   - `:lib` - All library files in the lib directory

2. **Library Target**:
   - `:system_libs` - AMD64-specific system libraries for static linking

## Included Libraries

The sysroot includes the following AMD64-specific libraries:

- Core system libraries:
  - glibc
  - gcc-unwrapped

- Compression libraries:
  - zlib
  - bzip2
  - xz

- XML and parsing:
  - libxml2
  - expat

- Networking:
  - openssl
  - curl

- Text processing:
  - pcre
  - pcre2

- JSON:
  - jansson

- Database:
  - sqlite

- Image processing:
  - libpng
  - libjpeg

- System utilities:
  - util-linux

## Usage in Bazel

This sysroot is typically used in conjunction with other sysroots:

```python
llvm.sysroot(
    name = "llvm_toolchain",
    targets = ["linux-x86_64"],
    label = "@bazel_sysroot_tarball_amd64//:sysroot",
    include_prefix = "@bazel_sysroot_library//:include",
    lib_prefix = "@bazel_sysroot_lib_amd64//:lib",
    system_libs = [
        "@bazel_sysroot_library//:system_deps",
        "@bazel_sysroot_library//:system_deps_static",
    ],
)
```

## Building

To build this sysroot:

```bash
nix-build default.nix
```

The output will be a directory containing the sysroot structure with all necessary files and the BUILD.sysroot.bazel file.