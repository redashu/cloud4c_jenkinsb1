# cloud4c_jenkinsb1

### info  jenkins 

<img src="info.png">

## Installing jenkins in Linux platform 

### login to linux machine 

```
  Downloads ssh -i "ashu-jenkins-key.pem" ec2-user@ec2-35-154-184-13.ap-south-1.compute.amazonaws.com  
The authenticity of host 'ec2-35-154-184-13.ap-south-1.compute.amazonaws.com (35.154.184.13)' can't be established.
ED25519 key fingerprint is SHA256:k/KOw9uMfkBMIato0bWOSRm6YbKpSrKCdUoEEanTu+E.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'ec2-35-154-184-13.ap-south-1.compute.amazonaws.com' (ED25519) to the list of known hosts.
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for 'ashu-jenkins-key.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "ashu-jenkins-key.pem": bad permissions
ec2-user@ec2-35-154-184-13.ap-south-1.compute.amazonaws.com: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
➜  Downloads 
➜  Downloads chmod 400 ashu-jenkins-key.pem
➜  Downloads 
➜  Downloads ssh -i "ashu-jenkins-key.pem" ec2-user@ec2-35-154-184-13.ap-south-1.compute.amazonaws.com  

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
[ec2-user@ip-172-31-41-190 ~]$ whoami
ec2-user
[ec2-user@ip-172-31-41-190 ~]$ sudo -i
[root@ip-172-31-41-190 ~]# whoami
root

```
