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

## For zVaultIO on FBSD 15.0 Build
See https://github.com/eekay35/zvio-15-build

