# BOSH Release for jumpbox

The `jumpbox` BOSH release sets up a jumpbox for use with BOSH/CF/Concourse, using a
docker image that installs utilities we've found to be generally useful for these 
tasks. You can also build your own docker-image to your custom specification and
use that, using our example Dockerfile in `docker/Dockerfile` or starting from scratch.


## Usage

To deploy a jumpbox, you can use the BOSH manifests supplied with the repository:

```
bosh -e <env> -d jumpbox --vars-file path/to/your/vars.yml deploy manifests/jumpbox.yml
```

Note that you *will* need to add users to your vars file, as otherwise there is no
way for you to log into the jumpbox. An example vars file is in `manifests/operations`,
along with various ops files to customize the deployment, if necessary. Other than adding
users, the defaults should be fine for most cases.
