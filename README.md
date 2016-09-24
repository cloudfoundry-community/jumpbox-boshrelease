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

- bosh-init 0.0.92-3ee9292
- cf 6.20
- curl 7.50.3
- genesis (latest and greatest!)
- git 2.10.0
- jq 1.5
- pwgen 2.07
- safe (latest and greatest!)
- shield
- spiff 1.0.7
- spruce (latest and greatest!)
- tmux 2.2
- tree 1.7.0
- unzip 6.0
- vault 0.5.2
- vim 7.4
- wget 1.18
- zip 3.0
