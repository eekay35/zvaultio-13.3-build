# About
This is just a simple patch to get zVaultIO built using the 13.3 repo.
Hopefully, more to come in the near future.

# Usage
NOTE: This should all be done as the root user to avoid any issues.

## For FBSD 13.3 Build
```
git clone https://github.com/zvaultio/zvio-build.git
cd zvio-build/
git checkout remotes/origin/zvio-13.3
fetch https://raw.githubusercontent.com/eekay35/zvaultio-13.3-build/refs/heads/main/zvaultio-13.5.patch -o zvaultio-13.5.patch
git apply zvaultio-13.5.patch
make bootstrap-pkgs
make checkout zvault
make release PROFILE=zvault PRODUCT=zVault Train=zVault-13
```

## For FBSD 15.0 Build
```
git clone https://github.com/zvaultio/zvio-build.git ./zvio-15-build
cd zvio-15-build/
git checkout remotes/origin/zvio-13.3
fetch https://raw.githubusercontent.com/eekay35/zvaultio-13.3-build/refs/heads/main/zvault-15.0.patch -o zvault-15.0.patch
git apply zvault-15.0.patch
make bootstrap-pkgs
make checkout zvault
fetch https://raw.githubusercontent.com/eekay35/zvaultio-13.3-build/refs/heads/main/zvault-15.0-middleware.patch -o zvault/_BE/zvio-middleware/zvault-15.0-middleware.patch
fetch https://raw.githubusercontent.com/eekay35/zvaultio-13.3-build/refs/heads/main/zvault-15.0-ports.patch -o zvault/_BE/zvio-ports/zvault-15.0-ports.patch
git -C zvault/_BE/zvio-middleware apply zvault-15.0-middleware.patch
git -C zvault/_BE/zvio-ports apply zvault-15.0-ports.patch
make release PROFILE=zvault PRODUCT=zVault Train=zVault-15
```

## Stuffs to deal with
Failures:

freenas/py-bsd@py311 | py311-bsd-: Failed: build
filesystems/openzfs | openzfs-2.4.1,1: Failed: configure
