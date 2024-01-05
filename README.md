
# Local Gitlab configuration

## Startup project

- Add on your /etc/hosts

```text
127.0.1.1	locallab
127.0.0.1   docker
```

- Init project

```sh
docker compose up -d
```

## New user on gitlab

- Create an user on the login page at http://locallab
- Login with `root` user and `testing1234` password
- Admit the new user and grant admin permisions on http://locallab/admin/users
- Login with your new user

## Enable docker socket (linux)

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


--executor docker --docker-image alpine:latest --docker-network-mode gitlab-network

