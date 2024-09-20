# This tutorial is solely for the CICD.
## Procedure :
<break>
        -Create a image on docker node 1 , push it to docker hub. <br> 
        -Pull image to node 2, and deploy it.    

## Pre requirement:
<break>
        -Docker install on both machine. <br>
        -Install java on both machine. Note that the java version must be the same for them. <br> 
        -Jenkins install on node 1: you can use package or run docker container 
    

## Config jenkins and setting the enviroment
<break>
        1. Run jenkins  on node 1 and access Jenkins( check systemctl status jenkins for more detail). Install nessesary plugin <br>
        2. Make a deploy node: 
            - Go to Dashboard - Manage Jenkins - Nodes 
            - Choose New node:  
                    + Enter Node name 
                    + Tick "Permanent Agent" then Next
                    + 
