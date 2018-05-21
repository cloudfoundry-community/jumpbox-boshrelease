# BOSH Release for jumpbox

The `jumpbox` BOSH release sets up a jumpbox for use with BOSH/CF/Concourse, using a
docker image that installs utilities we've found to be generally useful for these 
tasks. You can also build your own docker-image to your custom specification and
use that, using our example Dockerfile in `docker/Dockerfile` or starting from scratch.


## Usage

To deploy a jumpbox, you can use the BOSH manifests supplied with
the repository:

```
bosh -e <env> -d jumpbox deploy manifests/jumpbox.yml
```

However, that won't generally be enough, since you should
customize the configuration with your own user accounts and SSH
keys.  Here's a couple example ops files that you can modify and specify
with the `-o` option to `bosh deploy`:

An example ops file to use a custom default docker image would look like
```
---
- type: replace
  path: /instance_groups/name=jumpbox/jobs/name=jumpbox/properties/image/
  value: docker-registry.example.com/mygroup/jumpbox
```

An example of adding a user to the jumpbox.
```
---
- type: replace
  path: /instance_groups/name=jumpbox/jobs/name=jumpbox/properties/users/-
  value:
    name:  my-user-1                  # creates an account named `my-user-1`
    ssh_keys:
      - ssh-rsa my-key-here           # adds an ssh-key to the users authorized keys file
    image: busybox                    # overrides the global docker image for just this user
```

