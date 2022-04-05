# Integration Between Service

Prerequisites:

1. Repo created on GitLab
2. On jenkins connection to GitLab is setup with Personal Access Token

## 1. Jenkins and GitLab Integration

### 1. On gitlab create new Item

Give it a name and select freestyle project then click on "OK" button.
Give Description, then select your gitlab connection.
On Source Code Management select Git and fill the required field.
Repository URL is where your repo is being hosted.
Credentials is setup on Manage Jenkins > Configure System > Gitlab
