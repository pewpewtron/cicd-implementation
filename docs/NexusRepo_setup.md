# Run Nexus Repository OSS to your server

## 1. Run Nexus Repository OSS using container

```bash
podman run -d \
  --name nexus-service \
  -p 8081:8081 \
  -v nexus-volume:/nexus-data \
  sonatype/nexus3
```

To monitor setup proses run log command `podman logs -f nexus-service`

## 2. Initial Nexus Repository OSS setup
After container run try to access the nexus server using server ip
to find the password nexus password exec to container and find in /nexus-data/admin.password

```bash
podman exec -it nexus-service /bin/bash
cat /nexus-data/admin.password
```

login as admin and change password
`Redhat123!@#`

Click on settings on side bar click User and create new user

## 3. Setup Nexus for Container Registry
Click settings menu then on side bar click on Create repository then select `docker (hosted)`
Add Name, add HTTP connector by checking HTTP section then add port number to use, Enable Docker v1 API, 
Then create repository

After repository is created now configure Realms on setting menu select Realms on the side bar
then select Docker Bearer Token Realm, move it to Active