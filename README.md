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
sysutils/tw_cli | tw_cli-9.5.5_2: You must manually fetch the distribution file (CLI_freebsd-from_the_10-2-2-1_9-5-5-1_codesets.zip) from
https://docs.broadcom.com/docs-and-downloads/raid-controllers/raid-controllers-common-files/CLI_freebsd-from_the_10-2-2-1_9-5-5-1_codesets.zip,
place it in /distfiles/3dm2 and then run make again

Failures:

Logs: /usr/local/zvio-15-build/zvault/_BE/objs/ports/data/logs/bulk/ja-p/2026-04-14_18h42m58s

[00:00:15] Ignoring   sysutils/tw_cli | tw_cli-9.5.5_2: You must manually fetch the distribution file (CLI_freebsd-from_the_10-2-2-1_9-5-5-1_codesets.zip) from https://docs.broadcom.com/docs-and-downloads/raid-controllers/raid-controller
s-common-files/CLI_freebsd-from_the_10-2-2-1_9-5-5-1_codesets.zip, place it in /distfiles/3dm2 and then run make again

freenas/py-bsd@py311 | py311-bsd-: Failed: build
filesystems/openzfs | openzfs-2.4.1,1: Failed: configure

[00:08:11] [05] [00:00:51] Finished   freenas/zvio-py-bsd@py311 | py311-bsd-15.0_1737959244: Failed: build
[00:08:11] [05] [00:00:51] Skipping   freenas/freenas-files | freenas-files-15.0_1746400833: Dependent port freenas/zvio-py-bsd@py311 | py311-bsd-15.0_1737959244 failed                                                                     
[00:08:11] [05] [00:00:51] Skipping   freenas/freenas-migrate93 | freenas-migrate93-20191105: Dependent port freenas/zvio-py-bsd@py311 | py311-bsd-15.0_1737959244 failed                                                                    
[00:08:11] [05] [00:00:51] Skipping   freenas/py-midcli@py311 | py311-midcli-20190509171453: Dependent port freenas/zvio-py-bsd@py311 | py311-bsd-15.0_1737959244 failed                                                                     
[00:08:12] [05] [00:00:52] Skipping   freenas/py-middlewared@py311 | py311-middlewared-15.0_1746400833: Dependent port freenas/zvio-py-bsd@py311 | py311-bsd-15.0_1737959244 failed


