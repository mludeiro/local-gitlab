
# Local Gitlab configuration

## Enable docker socket:

- Create folder: /etc/systemd/system/docker.socket.d
- Create file 10-tcp.conf inside the folder with the content:

```text
[Socket]
ListenStream=0.0.0.0:2375
```

- restart everything:
```sh
systemctl daemon-reload
systemctl stop docker.socket
systemctl stop docker.service
systemctl start docker
```

## Extra parameters for docker runner cration

--executor docker --docker-image alpine:latest --docker-network-mode gitlab-network --tls-ca-file /etc/gitlab-runner/certs/cert.pem

