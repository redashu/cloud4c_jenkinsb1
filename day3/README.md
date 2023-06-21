# cloud4c_jenkinsb1

### Verify jenkins status 

```
[ec2-user@ip-172-31-41-190 ~]$ rpm -qa jenkins*
jenkins-2.401.1-1.1.noarch
[ec2-user@ip-172-31-41-190 ~]$ systemctl status jenkins
● jenkins.service - Jenkins Continuous Integration Server
   Loaded: loaded (/usr/lib/systemd/system/jenkins.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2023-06-21 03:39:19 UTC; 4min 10s ago
 Main PID: 3043 (java)
   CGroup: /system.slice/jenkins.service
           └─3043 /usr/bin/java -

===>
[ec2-user@ip-172-31-41-190 ~]$ grep jenkins /etc/passwd
jenkins:x:995:993:Jenkins Automation Server:/var/lib/jenkins:/bin/false
[ec2-user@ip-172-31-41-190 ~]$ 

```

## Integration of jenkins 

<img src="integrate.png">


### jenkins + docker integration cases

<img src="case1.png">

## Steps 

### installing docker on the same machine

```
ec2-user@ip-172-31-41-190 ~]$ sudo yum install docker -y
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core                                                                                                            | 3.7 kB  00:00:00     
Resolving Dependencies
--> Running transaction check
---> Package docker.x86_64 0:20.10.23-1.amzn2.0.1 will be installed
--> Processing Dependency: runc >= 1.0.0 for package: docker-20.10.23-1.amzn2.0.1.x86_64
--> Processing Dependency: libcgroup >= 0.40.rc1-5.15 f
```

### starting docker service 

```
[ec2-user@ip-172-31-41-190 ~]$ rpm -qa docker*
docker-20.10.23-1.amzn2.0.1.x86_64
[ec2-user@ip-172-31-41-190 ~]$ sudo systemctl start docker
[ec2-user@ip-172-31-41-190 ~]$ sudo systemctl enable  docker
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
[ec2-user@ip-172-31-41-190 ~]$ 
[ec2-user@ip-172-31-41-190 ~]$ sudo systemctl status   docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2023-06-21 04:05:58 UTC; 11s ago
     Docs: https://docs.docker.com
 Main PID: 18201 (dockerd)

```
