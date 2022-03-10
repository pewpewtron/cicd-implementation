# Deploy GitLab CE to your server

```bash
podman run -d -p 8080:8080 -p 50000:50000 --name jenkins_experiment --volume /home/jenkins-data:/var/jenkins_home  --network host jenkins/jenkins
```