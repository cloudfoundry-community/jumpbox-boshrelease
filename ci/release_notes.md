## Improvements

- New `jumpbox.env` property for setting global environment
  variables for all users on the jumpbox, as well as the startup
  script.

- The jumpbox job no longer requires Internet access to complete
  successfully - all packages have been included as real BOSH
  packages.

- This release is now (mostly) stemcell agnostic -- previous
  reliance on `apt-get` for package management is gone.
