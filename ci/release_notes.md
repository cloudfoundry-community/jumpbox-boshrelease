# Software Updates

- Upgraded `bosh` to 5.5.0
- Upgraded `cf` to 6.44.1
- Upgraded `cloudfoundry-utils` to 1.0.0
- Upgraded `credhub` to v2.4.0
- Upgraded `fly` to 5.1.0
- Upgraded `genesis` to 2.6.16

# Bug Fixes

- The `HOME` environment variable is now being set in the
  `inventory` errand, to allow both `genesis version` and `bosh
  -v` to succeed and provide versioning information.
