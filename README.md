# BOSH Release for jumpbox

The `jumpbox` BOSH release sets up a jumpbox for use with BOSH/CF/Concourse,
installing utilities we've found to be generally useful for these tasks, as
well as setting up custom user environments per user.

## Usage

To deploy a jumpbox, you can use the BOSH manifests supplied with the
repository.

```
bosh -e <env> -d jumpbox deploy manifests/jumpbox.yml
```

However, that won't generally be enough, since you should customize the
configuration with your own user accounts and SSH keys.  This repository
ships with an example ops file that you can modify to include your users,
environment setup scripts, and SSH keys.

To deploy that, use the `-o` option to `bosh deploy`:

```
bosh -e <env> -d jumpbox deploy \
  -o manifests/add-user-op.yml \
  manifests/jumpbox.yml
```

The following keys have meaning, for each user account under the
`jumpbox.users` parameter:

  1. `name` (**Required**) - The username for the account.

  2. `shell` - The full path to the user's interactive shell.
     This needs to be an allowed shell (per stemcell config).
     Defaults to `/bin/bash`.

  3. `sudo` (true|false) - Whether or not grant this user the
     ability to sudo as the root (or any other) user.
     Defaults to `false`.

  4. `password` - A (cleartext) password to set for the account.
     By default, users are not able to authenticate via any
     password (and should use `ssh_keys` instead).

  5. `ssh_keys` - A YAML list of SSH keys, in the form
     `algo key-data [comment]`.  Note that the comment
     (usually in the form "username@some.host") is optional,
     and has no bearing on the functionality of the key-based
     authentication.

  6. `env` - The URL of a git-clonable environment repo.
     For an example of what you might put in such a repository,
     see <https://github.com/jhunt/env>.
     By default, no environment repository is assumed.

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
- terraform 0.13.6
- unzip 6.0
- vault 0.5.2
- vim 7.4
- wget 1.18
- zip 3.0
