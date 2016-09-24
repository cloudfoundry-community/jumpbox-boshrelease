# BOSH Release for jumpbox

The `jumpbox` BOSH release sets up a jumpbox for use with BOSH/CF/Concourse, installing
utilities we've found to be generally useful for these tasks, as well as setting up
custom user environments per user.

## Usage

To create a generic template for bosh-lite:

`templates/make_manifest warden`

## Customizing Properties

```
properties:
  jumpbox:
    hostname: my-jumpbox-hostname      # sets hostname on the box
    users:
    - name: my-user-1                  # creates an account named `my-user-1`
      shell: /bin/bash                 # sets the account's shell to bash
      env: https://github.com/my/env   # clones a git repo of an environment to `~/env`
                                       # and runs `./install` from inside the repo, as
                                       # the user
      setup_script: /path/to/script    # runs after account creation, and environment
                                       # installation. the default value runs a script 
                                       # to set up rvm and install some ruby gems we 
                                       # find useful
      ssh_keys:
      - ssh-rsa my-key-here            # adds an ssh-key to the users authorized keys file
```


### Packages installed

- bosh-init
- cf
- curl
- genesis (latest and greatest!)
- git
- jq
- pwgen
- safe (latest and greatest!)
- shield
- spiff
- spruce (latest and greatest!)
- tmux
- tree
- unzip
- vault
- vim
- wget
- zip
