# DYNAMIC PROVISIONING OF SLAVE-NODES IN JENKINS CLUSTER USING DOCKER

![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/jenkins-docker.png?raw=true)


## WHAT IS DYNAMIC PROVISIONING?

##### Dynamic provisioning means provision of slave nodes as and when needed i.e. when we need to run any job in jenkins to save the resources


## Now let's try to implement this concept by integrating JENKINS with MAVEN using MASTER and SLAVE in Linux OS.


##### 1- Configure a Docker Host With Remote API :

Jenkins master connects to the docker host using REST APIs. So we need to enable the remote API for our docker host.

![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/remote-api.png?raw=true)

### step1:
Open the docker service file /lib/systemd/system/docker.service. Search for ExecStart and replace that line with the following.

```
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock
```

### step2:
Reload and restart docker service.

```
$ sudo systemctl daemon-reload
$ sudo service docker restart
```
### step3:
 Validate API by executing the following curl commands. Replace 54.221.134.7 with your host IP.

 ```
$ curl http://localhost:4243/version
$ curl http://54.221.134.7:4243/version
 ```

 ##### 2- Configure Jenkins Server With Docker Plugin : 

 - Head over to Jenkins Dashboard –> Manage Jenkins –> Manage Plugins.
![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/docker-plugin.png?raw=true)



- Head over cloud configuration under Manage Jenkins –> Manage Nodes and Clouds


![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/config-cloud.png?raw=true)

- Add docker Agent Template.


![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/docker-agent-template.png?raw=true)



#### Note:
 Replace “Docker URI” with your docker host IP. For example, tcp://10.128.0.3:4243 You can use the “Test connection” to test if Jenkins is able to connect to the Docker host.




 ###### 3- Job in Jenkins Setup :

 First we need plugins i.e. dependencies i.e. Git, Docker and Maven from Manage Jenkins --> Manage Plugins.

- Create New Freestyle Project:

![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/step1.png?raw=true)

- Now go to GENERAL and set options.

By-default job runs in master so we need to restrict it to run inside the slave-nodes.

![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/step2.png?raw=true)


- Now go to SOURCE CODE MANAGEMENT and set options.

Here we take code from GitHub for testing purpose.

![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/step3.png?raw=true)

- Now go to BUILD and set options.

We need to perform operations i.e. Test --> Compile --> Package.


![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/step4.png?raw=true)

- Now go to POST BUILD ACTIONS and set options.

As we want to archive the package i.e. called ARTIFACT to download it in .jar extension to use it directly.

![jenkins-docker](https://github.com/OussamaMaroufi/Dynamic-provisioning-of-slave-node-jenkins/blob/main/images/step5.png?raw=true)










