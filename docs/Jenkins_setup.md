# Run GitLab CE to your server

## 1. Run GitLab CE using container

```bash
podman run -d \
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
