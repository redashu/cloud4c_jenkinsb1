# cloud4c_jenkinsb1

## Revision 

<img src="rev.png">

### how run jenkins in a container to avoid installation 

```
[root@ip-172-31-12-245 ~]# docker run -itd --name jenkins -p 8080:8080 -v jenkins_data:/var/jenkins_home --restart always jenkins/jenkins:lts-jdk11  
Unable to find image 'jenkins/jenkins:lts-jdk11' locally
lts-jdk11: Pulling from jenkins/jenkins
bd73737482dd: Pull complete 
747b9186aa97: Pull complete

```

### checking default password for installation 

```
root@ip-172-31-12-245 ~]# docker logs jenkins 
Running from: /usr/share/jenkins/jenkins.war
webroot: /var/jenkins_home/war
2023-06-23 03:47:38.577+0000 [id=1]	INFO	winstone.Logger#logInternal: Beginning extraction from war file
2023-06-23 03:47:39.836+0000 [id=1]	WARNING	o.e.j.s.handler.ContextHandler#setContextPath: Empty contextPath
2023-06-23 03:47:39.911+0000 [id=1]	INFO	org.eclipse.jetty.server.Server#doStart: jetty-10.

*************************************************************
*************************************************************

Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

895cf5d450784d229f0f5af0b25c3156

This may also be found at: /var/jenkins_home/secrets/initialAdminPassword



```
