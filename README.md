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

The versions below are illustrative. `INCLUDES.yml` is the source of
truth for what each release actually ships.

golang-1-linux:
- go 1.latest
jumpbox:
- curl (on stemcell)
- git 2.54.0
- tmux 3.6b
  - libevent 2.1.12
- tree 2.3.2
- vim 9.2.0541
- wget 1.25.0
- s3cmd 2.4.0
- zip / unzip (on stemcell)

Precompiled binaries / scripts:
- jumpbox/bins/
  - bbr 1.9.78
  - bosh 7.10.5
  - certstrap 1.3.0
  - cf 8.18.3 (cf8 alias)
  - credhub 2.9.57
  - esuf 0.1.2
  - fly 8.2.3
  - genesis 3.0.14
  - jq 1.8.1
  - nats 1.0.2
  - safe 1.9.0
  - shield 9.0.1
  - spiff 1.0.8
  - spruce 1.35.7
  - terraform 1.5.7
  - tofu 1.12.1
  - tmate 2.4.0
  - uaa 0.20.2
  - vault 1.14.10
  - bao 2.5.4
  - yq 4.53.2
