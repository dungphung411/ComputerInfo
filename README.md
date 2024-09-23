# This tutorial is solely for the CICD.
## Procedure :
<break>
        -Create a image on docker node 1 , push it to docker hub. <br> 
        -Pull image to node 2, and deploy it.    

## Pre requirement:
<break>
        -Docker install on both machine. <br>
        -Install java on both machine. Note that the java version MUST be the same for them. (Rec 17, 21) <br> 
        -Jenkins install on node 1
    

## Config jenkins and setting the enviroment
<break>
        1. Run jenkins  on node 1 and access Jenkins( check systemctl status jenkins for more detail). Install nessesary plugin <br>
            - Continue to install SonarQube, SonnarScaner, Docker, ... plugin  
        2. Make a deploy node: <br>
            - Go do Dashboard - Manage Jenkins - Sercurity - Scroll dowm untill you see 'Agents' - Choose 'fixed tcp port' and enter the port 8889 - Apply and save. <br>
            - Go back to Dashboard - Manage Jenkins - Nodes <br>
            - Choose New node:  <br>
                    + Enter Node name <br>
                    + Tick "Permanent Agent" then Next <br>
                    + 
