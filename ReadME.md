# Config Manager
A simple tool to facilitates the management of configuration changes on bare-metal infrastructure.

# Prerequisite
We need following tools to run this project
- Docker
- Docker compose
- openjdk-17-jdk (for slave as Jenkins runs on java)

# Limitations

- File deletions is not handled and ignored.
- It is tested on Ubuntu Operating System.

# Components

Jenkins is used for ci/cd
Jenkins has vault integrated (done via UI) and Vault stores all the ssh user credentials

# Installation Setup

**Step 1** Required: Clone this repository using git.
```bash
git clone https://github.com/Svastikkka/CONFIG-MANAGER.git
```

**Step 2** Required: Go inside the repository
```bash
cd ./CONFIG-MANAGER
```

**Step 3** Required: Run the below command to initialize intial setup (If we are initializing without any previous/existing data)
```bash
docker compose up -d
```

**Step 4** Optional: Run the below command to initialize intial setup (If we are initializing with any previous/existing data)

**Step 4.1** Restore backups in below directories
- jenkins_home (need to create it manually)
- vault (need to create it manually)

**Step 4.2** Run the below command to start Jenkins and Vault
```bash
docker compose up -d
```

**Step 5** Required: Check services are UP

**Step 5.1** Check Vault is UP by going on the following URL: http://COMP_PRIVATE_IP:8200.  We should able to see its UI

**Step 5.2** Check Jenkins is UP by going on the following URL: http://COMP_PRIVATE_IP:8080.  We should able to see its UI

**Step 6** Required: Configure Jenkins to install default Plugins.

*Reference*: We can go through following video to understand [How to Install Jenkins on Ubuntu Linux](https://www.youtube.com/watch?v=s1o9BKW2rdw)

**Step 7** Required: Unseal Vault

**Step 8** Required: Enable approle in vault

**Step 9** Required: Enable KV in vault

**Step 10** Required: Install Required Plugins in Jenkins
1. Pipeline Utility Steps
2. Vault Plugin
3. Gitlab

*Reference*: [How to Install Jenkins Plugins](https://www.youtube.com/watch?app=desktop&v=JX_G2gAGvfk)

*Reference*: [Managing Plugins](https://www.jenkins.io/doc/book/managing/plugins/)

**Step 11** Required: Integrate Jenkins with Vault

Navigate to manage Jenkins and Configure system. and find the vault plugin and fill the URL and then click on add the credentilas to add the approle authentication and select kind as Vault AppRole Credentials and fill out the role ID, Secret ID, path and ID as generic name to identify and click on Add.

*Note*: On advance settings disable the ssl certfication.

*Reference* [How to Integrate HashiCorp Vault With Jenkins](https://www.youtube.com/watch?v=5-RMu9M_Anc)

**Step 12** Create a Job
Try to create a Job Config Manager with type **pipeline** and add **Config Manager** repository URL and Trigger it manually.

# Reference

- [How to Integrate Gitlab with Jenkins using SSH Connection](https://www.youtube.com/watch?v=fE741bkK1kA)
- [Slave Connection](https://community.jenkins.io/t/node-connection-error/6082)
- [How to Integrate HashiCorp Vault With Jenkins](https://www.youtube.com/watch?v=5-RMu9M_Anc)
- [How to Install Jenkins Plugins](https://www.youtube.com/watch?app=desktop&v=JX_G2gAGvfk)
- [Managing Plugins](https://www.jenkins.io/doc/book/managing/plugins/)
- [Role-based Authorization Strategy](https://plugins.jenkins.io/role-strategy/)
