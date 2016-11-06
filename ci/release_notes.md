## New Features

- Per-user setup is now handled on a per-user basis, via a
  one-time setup script embedded in their ~/.bashrc / ~/.zshrc
  profiles.  This should greatly speed up provisioning.

- You can now set the jumpbox login banner, via `jumpbox.banner`
  It's got a spiffy default too!

## Improvements

- Default `$PATH` now puts the jumpbox package bin directory
  first, so that release-provided software like `curl` and `vim`
  takes precedence over system versions.

- New sane default configuration for `vim` and `tmux`

- New `acceptance-tests` job for verifying the viability of the
  Jumpbox BOSH release itself.  This will be used in our CI
  pipelines moving forward, to ensure that all utilities work
  out of the box.

##### safe
Bumped safe to v0.0.26
