# pkgs

![Dependency Diagram](/deps.png)

This repository produces a set of packages that can be used to build a rootfs suitable for creating custom Linux distributions.
The packages are published as a container image, and can be "installed" by simply copying the contents to your rootfs.
For example, using Docker, we can do the following:

```docker
FROM scratch
COPY --from=<registry>/<organization>/<pkg>:<tag> / /
```

## Resources

- https://gcc.gnu.org/onlinedocs/gccint/Configure-Terms.html
- https://wiki.osdev.org/Target_Triplet

## Rock 5 WIP

*WARNING*: This repository will be rebased when needed

### Changes

- update Linux to collabora rk3588-v6.8: basic support for Rock 5B

### Current status

Builds fine using `make kernel USERNAME=choopm PLATFORM=linux/arm64 PUSH=true`.

This will create `ghcr.io/choopm/kernel:$TAG` which can be used by other Talos tools for creating boot assets:

```bash
# run from https://github.com/siderolabs/talos

make imager \
    USERNAME=choopm \
    PKG_KERNEL=ghcr.io/choopm/kernel:$TAG \
    PLATFORM=linux/arm64 \
    INSTALLER_ARCH=arm64 \
    PUSH=true

make installer \
    USERNAME=choopm \
    PKG_KERNEL=ghcr.io/choopm/kernel:$TAG \
    PLATFORM=linux/arm64 \
    INSTALLER_ARCH=arm64 \
    PUSH=true
```
