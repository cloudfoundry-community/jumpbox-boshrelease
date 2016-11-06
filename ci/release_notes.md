## Improvements

- User home directories are now in /u/$name, so that `bosh-init`
  doesn't fail to deploy things like ruby-based CPIs that rely on
  gem + bundler.  It's not LSB, but it's ok

- SSH Host Keys will now persist across VM recreation, so you can
  start trusting your SSH Host Key mismatch warnings again, and
  maybe even re-enable strict host key checking!

- Some UNIX trickery was added to ensure that UID/GIDs stayed the
  same across BOSH recreates and VM resurrection, so that people
  don't lose ownership to files outside their home directories due
  to UID/GID re-assignment.

- One-time per-user setup is now no longer triggered for the
  `vcap` user, or for any of the temporary accounts created for
  `bosh ssh` sessions.

## Bug Fixes

- Handle utilities that don't send their version information to
  standard output, like `safe`.  Redirecting stderr makes the
  output of the errand look muuuuuuch nicer.
