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

This step could take a while, to monitor the progress of the container run the following command: `podman logs -f gitlab-service`

## 3. Gitlab setup

After the container run try to access the gitlab server using server ip and login using root email and password that define earlier.

## 4. Create new user and Personal Access Token for Jenkins integration

Login as admin then select menu then Admin > Users > New User > Create new user

```yaml
gitlab_user:
  name: "jenkins-user"
  username: "Redhat123!@#"
```

note: you also can use admin/root user Personal access token to simplified the process.

After new user is created now login as said user and create a Personal Access Token from User Settings > Access Tokens

```yaml
gitlab-jenkins-token: "yKixv6zzmds5QzExRrNn"
gitlab-admin-token: "gcP9e-wka2kGX8CA44s9"
```

## 5. Create new repo
