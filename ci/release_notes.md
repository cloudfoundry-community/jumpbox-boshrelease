# Bug Fixes

- umask is now forcibly set to 022, so that newly-created account
  home directories are set properly as mode 0755, instead of 0775.
