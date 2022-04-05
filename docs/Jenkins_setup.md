# Run GitLab CE to your server

## 1. Run GitLab CE using container

```bash
podman run -dt \
  --name jenkins-service \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins-volume:/var/jenkins_home \
  jenkins/jenkins
```

## 2. Jenkins setup

1. after the container run try to access the jenkins server

2. Get initial password from the jenkins log or access it from the jenkins server

```bash
podman logs jenkins-service | grep 'Initial password'

podman exec jenkins-service -it /bin/bash
cat /var/jenkins_home/secrets/initialAdminPassword
```

`34425f8f938c4a95ae32107652ad6190`

## 3. Login to jenkins

After get the password from the jenkins log or access it from the jenkins server
Install all suggested plugins
Create root user

```yaml
username: root
password: Redhat123!@#
```

## 3. Install required plugin

Install following plugin

- GitLab
- Job DSL

## 4. Add Gitlab Personal Access Tokens

Add GitLab Personal Access Tokens to jenkins
on Jenkins Dashboard > Manage Jenkins > Configure system > search for GitLab
add new connection name, GitLab host URL, and add credential.
on add credential popup select kind dropdown and use GitLab API token
after credential added test the connection.
