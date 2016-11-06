## Improvements

- User home directories are now in /u/$name, so that `bosh-init`
  doesn't fail to deploy things like ruby-based CPIs that rely on
  gem + bundler.  It's not LSB, but it's ok
