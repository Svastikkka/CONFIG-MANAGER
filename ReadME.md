# Config Server
A simple tool to facilitates the management of configuration changes on bare-metal infrastructure.

# Prerequisite
We need following tools to run this project
- Docker
- Docker compose
- openjdk-17-jdk (for slave as Jenkins runs on java)

# Limitations

File deletions is not handled and ignored.

# Components

Jenkins is used for ci/cd
Jenkins has vault integrated (done via UI) and Vault stores all the ssh user credentials

# Installation Setup