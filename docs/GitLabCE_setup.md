# Deploy GitLab CE to your server


## 1. Prepare location for persistent storage
Create a directory for GitLab CE to store its data.

```bash 
mkdir -p /home/gitlab/data
mkdir -p /home/gitlab/logs
mkdir -p /home/gitlab/config

export GITLAB_HOME=/home/gitlab
```
Table below explaining required and propose of each directory:
| Local location | Container location | Usage |
| ------------- |:-------------:| -----:|
| `$GITLAB_HOME/data` | `/var/opt/gitlab` | For storing application data |
| `$GITLAB_HOME/logs` | `/var/log/gitlab` | For storing logs |
| `$GITLAB_HOME/config` | `/etc/gitlab` | For storing the GitLab configuration files |

## 2. Install GitLab CE using 
Either with docker or podman run following command to pull gitlab-ce image and run it on the server.

```bash
podman run --detach \
  --hostname dev.example.com \
  --publish 443:443 --publish 80:80 --publish 22:22 \
  --name gitlab-service \
  --restart always \
  --volume $GITLAB_HOME/config:/etc/gitlab:Z \
  --volume $GITLAB_HOME/logs:/var/log/gitlab:Z \
  --volume $GITLAB_HOME/data:/var/opt/gitlab:Z \
  -e GITLAB_ROOT_EMAIL="root@local" \
  -e GITLAB_ROOT_PASSWORD="Redhat123" \
  --shm-size 256m \
  gitlab/gitlab-ce:latest
```
