# DYNAMIC PROVISIONING OF SLAVE-NODES IN JENKINS CLUSTER USING DOCKER

![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/jenkins-docker.png?raw=true)


## WHAT IS DYNAMIC PROVISIONING?

##### Dynamic provisioning means provision of slave nodes as and when needed i.e. when we need to run any job in jenkins to save the resources


## Now let's try to implement this concept by integrating JENKINS with MAVEN using MASTER and SLAVE in Linux OS.


##### Configure a Docker Host With Remote API :

Jenkins master connects to the docker host using REST APIs. So we need to enable the remote API for our docker host.

![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/remote-api.png?raw=true)
