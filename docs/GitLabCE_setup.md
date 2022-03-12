# Run GitLab CE to your server

## 1. Prepare location for persistent storage

Create a directory for GitLab CE to store its data.

```bash
mkdir -p /srv/gitlab/data
mkdir -p /srv/gitlab/logs
mkdir -p /srv/gitlab/config

export GITLAB_HOME=/srv/gitlab
```

Table below explaining required and propose of each directory:
| Local location | Container location | Usage |
| ------------- |:-------------:| -----:|
| `$GITLAB_HOME/data` | `/var/opt/gitlab` | For storing application data |
| `$GITLAB_HOME/logs` | `/var/log/gitlab` | For storing logs |
| `$GITLAB_HOME/config` | `/etc/gitlab` | For storing the GitLab configuration files |

## 2. Run GitLab CE using container

Either with docker or podman run following command to pull gitlab-ce image and run it on the server.

```bash
podman run -d \
  --name gitlab-service \
  --restart always \
  --hostname dev.example.com \
  -p 443:443 -p 80:80 -p 222:22 \
  -v $GITLAB_HOME/config:/etc/gitlab:Z \
  -v $GITLAB_HOME/logs:/var/log/gitlab:Z \
  -v $GITLAB_HOME/data:/var/opt/gitlab:Z \
  -e GITLAB_ROOT_EMAIL="root@local" \
  -e GITLAB_ROOT_PASSWORD="Redhat123" \
  --shm-size 256m \
  gitlab/gitlab-ce:latest
```

## 3. Gitlab setup
