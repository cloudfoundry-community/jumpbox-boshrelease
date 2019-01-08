# Bug Fixes

- The bundled copy of jq 1.5 is now sourced from a precompiled
  64-bit Linux binary, and includes full regular expressions
  support.

- New users are now added to the BOSH `vcap` group, in addition to
  `staff`.

- SSH authorized_keys files are refreshed after deployments if any
  changes were made

- Added `--with-ssl=openssl` to wget configure to support installation 
  on xenial (backwards compatible with trusty)

# Changes

- SSH Keys are now properly cleared if rotated or removed from the manifest. This makes the deployment manifest the source of truth for auth and ensures that when keys are removed from the manifest they are also removed as valid for the user.

# Software Updates

- *terraform* upgraded to 0.11.11
- *credhub* upgraded to 1.7.7
- *fly* (Concourse) upgraded to 4.2.2
- *git* upgraded to 2.19.2 (Nov 2018)
- *safe* upgraded to v0.9.9
- *cf* upgraded to v6.41.0
