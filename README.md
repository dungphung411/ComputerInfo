# This tutorial is solely for the CICD.
## Procedure :
-  Create a image on docker node 1 , push it to docker hub. 
-  Pull image to node 2, and deploy it.    

## Pre requirement:
- Docker install on both machine. 
- Install java on both machine. Note that the java version **MUST** be the same for them. (Rec 17, 21)  
- Jenkins install on node 1
    

## Config jenkins and setting the enviroment
1. *Run jenkins  on node 1 and access Jenkins*
- Check systemctl status jenkins for more detail. 
- Install nessesary plugin 
- Continue to install SonarQube, SonnarScaner, Docker, ... plugin  
2. *Make a deploy node:*
- Go do Dashboard - Manage Jenkins - Sercurity - Scroll dowm untill you see 'Agents' - Choose 'fixed tcp port' and enter the port 8889 - Apply and save.
- Go back to Dashboard - Manage Jenkins - Nodes 
- Choose New node:   Enter Node name - Tick "Permanent Agent" then Next - **MUST** provide label for your node 
    ![nodes](nodes.png)
- Apply and save
3. *Create a pipeline*
- New Iteam - Pipeline - Give it a name 
- Tick discard old build - Better max build to keep is lower than 3 
- Pipeline - Choose pipeline from SCM - Git - Enter the repo URL - no credential - choose brach 'Work-on-2-node' - Apply and save

## The Jenkinsfile modifies
- Include label agent in each stage is a must 
- There're 2 label in the jenkinsfile: 
-           agent {label 'Main'} 
            agent { label '10.32.4.107' }
- Main is the jenkins server aka node 1, 10.32.4.107 is the node 2 
- Change the name to the label you name before.