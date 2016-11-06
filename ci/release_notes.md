## Improvements

- User home directories are now in /u/$name, so that `bosh-init`
  doesn't fail to deploy things like ruby-based CPIs that rely on
  gem + bundler.  It's not LSB, but it's ok

- SSH Host Keys will now persist across VM recreation, so you can
  start trusting your SSH Host Key mismatch warnings again, and
  maybe even re-enable strict host key checking!
