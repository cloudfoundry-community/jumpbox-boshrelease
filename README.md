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
