# Tool Versions

All bundled tools, compared against the previous release (v5.1.2):

| Tool      | v5.1.2    | This release | Notes                                    |
|-----------|-----------|--------------|------------------------------------------|
| bao       | —         | 2.5.4        | New — OpenBao, open-source Vault fork    |
| bbr       | 1.9.76    | 1.9.79       |                                          |
| bosh      | 7.9.18    | 7.10.7       |                                          |
| certstrap | 1.2.0     | 1.3.0        |                                          |
| cf        | 6.53.0    | 8.18.3       | cf v6 and v7 dropped; `cf` is now CLI v8 |
| cf7       | 7.8.0     | —            | Removed                                  |
| cf8       | 8.17.1    | 8.18.3       | Alias of `cf`                            |
| credhub   | 2.9.54    | 2.9.58       |                                          |
| esuf      | 0.1.2     | 0.1.2        |                                          |
| fly       | 8.0.2     | 8.2.4        |                                          |
| genesis   | 3.0.14    | 3.0.14       |                                          |
| git       | 2.35.7    | 2.54.0       |                                          |
| jq        | 1.6       | 1.8.1        |                                          |
| nats      | 1.0.2     | 1.0.2        |                                          |
| s3cmd     | 2.4.0     | 2.4.0        | Install fixed — see below                |
| safe      | 1.9.0     | 1.9.0        |                                          |
| shield    | 8.7.4     | 9.0.1        |                                          |
| spiff     | 1.0.8     | 1.0.8        |                                          |
| spruce    | 1.31.1    | 1.35.11      |                                          |
| terraform | 1.1.7     | 1.5.7        | Last MPL-2.0 release (pre-BSL)           |
| tmate     | 2.4.0     | 2.4.0        |                                          |
| tmux      | 3.2a      | 3.6b         |                                          |
| tofu      | —         | 1.12.1       | New — OpenTofu, open-source Terraform fork |
| tree      | 2.0.2     | 2.3.2        |                                          |
| uaa-cli   | 0.16.0    | 0.20.2       |                                          |
| vault     | 1.9.4     | 1.14.10      | Last MPL release before BSL relicense    |
| vim       | 8.2.4528  | 9.2.0597     | Now shipped prebuilt, not compiled       |
| wget      | 1.21.3    | 1.25.0       |                                          |
| yq        | (unrecorded) | 4.53.2    | Previous version not tracked             |

# s3cmd

- Fixed s3cmd being installed outside the package bin directory on jammy/noble
  stemcells. Debian-patched pip routes `--prefix` installs to
  `$PREFIX/local/{bin,lib}` (posix_local scheme), so s3cmd and its `S3` module
  were never on PATH. s3cmd is now installed with `pip install --target` and
  exposed through a PYTHONPATH wrapper script. (#113)

# jumpbox

- Fixed job logging: output now lands in `/var/vcap/sys/log/jumpbox/jumpbox.log`,
  and `/etc` restoration is skipped on the watcher's first run to avoid
  uid/gid mismatches after stemcell changes. (#109)
- Added initial support for Ubuntu Noble stemcells.

# inventory

- Expanded the inventory errand to verify every bundled tool, adding checks
  for uaa, esuf, terraform, tofu, bao, certstrap, yq, nats, and s3cmd.
- The inventory errand now prints the command output when a check fails,
  instead of discarding it, so failures can be diagnosed from the errand
  logs. (#113)
