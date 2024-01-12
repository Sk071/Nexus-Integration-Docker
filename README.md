# Nexus-Integration-Docker
sonatype/nexus3 integration using docker file for cicd pipeline using jenkins

********************************************************************************

use folowing commands to run docker image 

docker volume create --name nexus-data

docker run -d -p 8081:8081 --name nexus -v nexus-data:/nexus-data sonatype/nexus3

After the container is running, you can find the admin.password file in the /nexus-data folder. This file contains the default password for the admin user:

docker exec -it nexus /bin/bash
cat /nexus-data/admin.password


aa390e46-029a-49e6-acf3-8ac88e443c15
