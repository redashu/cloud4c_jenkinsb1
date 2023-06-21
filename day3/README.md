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
