# BOSH Release for jumpbox

This is BOSH release for jumpbox with BOSH cli with BOSH bootstrap and workspace installed.

## Usage

To use this bosh release, first upload it to your bosh:

```
bosh target BOSH_HOST
git clone https://github.com/cloudfoundry-community/jumpbox-boshrelease.git
cd jumpbox-boshrelease
bosh upload release releases/jumpbox-1.yml
```

For [bosh-lite](https://github.com/cloudfoundry/bosh-lite), you can quickly create a deployment manifest & deploy a cluster:

```
templates/make_manifest warden
bosh -n deploy
```

For AWS EC2, create a single VM:

```
templates/make_manifest aws-ec2
bosh -n deploy
```

### Override security groups

For AWS & Openstack, the default deployment assumes there is a `default` security group. If you wish to use a different security group(s) then you can pass in additional configuration when running `make_manifest` above.

Create a file `my-networking.yml`:

``` yaml
---
networks:
  - name: jumpbox1
    type: dynamic
    cloud_properties:
      security_groups:
        - jumpbox
```

Where `- jumpbox` means you wish to use an existing security group called `jumpbox`.

You now suffix this file path to the `make_manifest` command:

```
templates/make_manifest openstack-nova my-networking.yml
bosh -n deploy
```

### Packages installed

- spiff (1.0.6)
- bosh (1.2922.0)
- uaac (1.3.1)
- cf (6.11.1)
- bosh-bootstrap (0.16.2)
- bosh-workspace (0.9.0.rc4)
- ruby (2.1.6)
