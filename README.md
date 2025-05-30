# Bazel Library Sysroot for AMD64

This repository contains a collection of system libraries and headers for AMD64 architecture that can be used with Bazel builds. Built using Nix, it provides a consistent set of system dependencies across different environments.

## Available Make Targets

- `make help` - Show available targets and their descriptions
- `make update-flake` - Update flake.lock with latest dependencies
- `make build` - Build the AMD64 library sysroot using nix build
- `make tarball` - Create a .tar.gz archive of the AMD64 library sysroot
- `make nix-tarball` - Create a .tar.gz archive using nix build
- `make copy` - Copy files from Nix store to sysroot directory
- `make push` - Push changes to GitHub with dated commit
- `make update-all` - Update flake, build, copy, and push
- `make clean` - Clean up build artifacts

## Repository Structure

```
.
├── default.nix      # Nix package definition
├── flake.nix        # Nix flake configuration
├── Makefile         # Build and maintenance targets
├── sysroot/         # Sysroot files (generated)
│   ├── include/     # System header files
│   └── lib/         # System library files
└── .gitignore      # Git ignore rules
```

## Included Libraries

The sysroot includes the following system libraries and their development files:

- Core system libraries (glibc, gcc)
- Compression libraries (zlib, bzip2, xz)
- XML and parsing (libxml2, expat)
- Networking (openssl, curl)
- Text processing (pcre, pcre2)
- JSON (jansson)
- Database (sqlite)
- Image processing (libpng, libjpeg)
- System utilities (util-linux)

## Usage

1. Build the sysroot:
   ```bash
   make build
   ```

2. Copy files to the repository:
   ```bash
   make copy
   ```

3. Create a tarball:
   ```bash
   make tarball
   # or
   make nix-tarball
   ```

4. Update everything and push:
   ```bash
   make update-all
   ```

## Dependencies

- Nix package manager
- rsync (for copying files)
- git (for version control)

## Bazel Integration

The sysroot provides two main targets in its BUILD file:

- `system_deps`: For dynamic linking (shared libraries)
- `system_deps_static`: For static linking (static libraries)

Example usage in a Bazel BUILD file:
```python
cc_library(
    name = "my_library",
    srcs = ["my_library.cpp"],
    deps = ["@bazel_sysroot_lib_amd64//sysroot:system_deps"],
)
```