# BOSH Release for jumpbox

The `jumpbox` BOSH release sets up a jumpbox for use with BOSH/CF/Concourse, installing
utilities we've found to be generally useful for these tasks, as well as setting up
custom user environments per user.

## Usage

To deploy a jumpbox, you can use the BOSH manifests supplied with
the repository:

```
bosh -e <env> -d jumpbox deploy manifests/jumpbox.yml
```

However, that won't generally be enough, since you should
customize the configuration with your own user accounts and SSH
keys.  Here's an example ops file that you can modify and specify
with the `-o` option to `bosh deploy`:

```
---
- type: replace
  path: /instance_groups/name=jumpbox/jobs/name=jumpbox/properties/users/-
  value:
    name:  my-user-1                  # creates an account named `my-user-1`
    shell: /bin/bash                  # sets the account's shell to bash
    env:   https://github.com/my/env  # clones a git repo of an environment to `~/env`
                                      # and runs `./install` from inside the repo, as
                                      # the user
    setup_script: /path/to/script     # runs after account creation, and environment
                                      # installation. the default value runs a script
                                      # to set up rvm and install some ruby gems we
                                      # find useful
    ssh_keys:
      - ssh-rsa my-key-here           # adds an ssh-key to the users authorized keys file
```

If you don't want a user to have sudo access, set `sudo: no` on
their user account, and they will not be granted it.

## Taking Inventory

The `inventory` job is an errand you can colocate on your
jumpboxen.  It will display information about the software
installed on the instance, versions, etc.


### Packages installed

- bosh-init 0.0.92-3ee9292
- cf 6.30
- curl 7.50.3
- genesis (latest and greatest!)
- git 2.14.1
- jq 1.5
- safe (latest and greatest!)
- shield
- spiff 1.0.7
- tmux 2.2
- tree 1.7.0
- unzip 6.0
- vault 0.5.2
- vim 7.4
- wget 1.18
- zip 3.0
