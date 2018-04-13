# Improvements

- This release no longer mucks with /etc/sudoers; it just
  provisions users into the `bosh_sudoers` group.

- New `jumpbox.ssh_password_auth` property, to enable (or disable)
  SSHd password authentication.

- Users can now have passwords created for them, although this
  mode of operation is higly discouraged.

- You can remove sudo privileges from individual accounts, by
  setting `sudo: no` in their user definition.

# New Software

- Added credhub-cli v1.6.0
- Added fly-cli v3.9.1
