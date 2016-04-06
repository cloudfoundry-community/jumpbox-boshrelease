# v4 Release

`jumpbox-boshrelease` now does actual jumpbox-y things!

This release auto-installs a bunch of utilities we find
that we're always using on our jumpboxen, to make dealing with
bosh easier. These things include, but are not limited to:

- golang
- ruby/rvm
- bosh_cli
- bosh-workspace
- cf-uaac
- cf cli
- spruce
- spiff
- vault
- safe
- genesis
- tmux
- tree
- git

And more!

You can use this release for customizing your jumpbox as well.
To set the hostname of the box, set the `jumpbox.hostname` property.
Users can be added (with persistent home directories, custom
environments, ssh keys, shells, and more) via the `jumpbox.users`
list:

```
properties:
  jumpbox:
    users:
    - name: myuser
      shell: /bin/bash
      env: https://github.com/myuser/my-env-repo # runs `./install` from inside the repo to install it
      setup_script: /path/to/generic/user/setup
      ssh_keys:
      - ssh-rsa my-key-here
```
