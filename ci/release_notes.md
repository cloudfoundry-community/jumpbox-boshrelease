# Software Components

## Updated to be compatible with Ubuntu Jammy stemcells

This release requires ubuntu-jammy stemcells; if you require ubuntu-bionic,
you must use an v4.x.x version.

## Updated compiled versions of jumpbox binaries

- Bumped bbr to v1.9.53
- Bumped bosh-cli to v7.4.1
- Bumped cf7 to v7.7.4
- Bumped cf8 to v8.7.4
- Bumped credhub to v2.9.22
- Bumped fly to v7.11.0
- Bumped genesis to v2.8.11
- Bumped safe to v1.9.0
- Bumped spruce to v1.31.0

## Use utilities from jammy stemcell

The following were explicitly downloaded and compiled from source, but the
current version on the jammy stemcells are the same version and will get
updates from future versions of the stemcells.

- curl
- zip
- unzip

## Updated golang to v1.21.4
