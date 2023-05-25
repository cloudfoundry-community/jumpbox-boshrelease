Enable configuration of jumpbox `/etc/ssh/sshd_config` parameters:

- `ClientAliveInterval` via `properties.jumpbox.ssh.client_alive_interval` with a default value of 1200
- `ClientAliveCountMax` via `properties.jumpbox.ssh.client_alive_count_max` with a default value of 3.

Together these give a default session timeout of 1 hour.

