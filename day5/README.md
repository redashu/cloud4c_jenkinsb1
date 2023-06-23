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

### Understanding prod grade jenkins and executors

<img src="exe.png">

### we can change executors number 

```
[root@ip-172-31-41-190 ~]# cd /var/lib/jenkins/
[root@ip-172-31-41-190 jenkins]# ls
%C                                           jenkins.model.JenkinsLocationConfiguration.xml             queue.xml.bak
config.xml                                   jenkins.telemetry.Correlator.xml                           secret.key
credentials.xml                              jobs                                                       secret.key.not-so-secret
fingerprints                                 logs                                                       secrets
hudson.model.UpdateCenter.xml                nodeMonitors.xml                                           updates
hudson.plugins.git.GitTool.xml               nodes                                                      userContent
identity.key.enc                             org.jenkinsci.plugins.workflow.flow.FlowExecutionList.xml  users
jenkins.install.InstallUtil.lastExecVersion  plugins                                                    workspace
jenkins.install.UpgradeWizard.state          queue.xml
[root@ip-172-31-41-190 jenkins]# 
[root@ip-172-31-41-190 jenkins]# 
[root@ip-172-31-41-190 jenkins]# grep -in exec  config.xml 
5:  <numExecutors>2</numExecutors>
28:      <filterExecutors>false</filterExecutors>
35:      <filterExecutors>false</filterExecutors>
[root@ip-172-31-41-190 jenkins]# lscpu  | grep -i cpu 
CPU op-mode(s):      32-bit, 64-bit
CPU(s):              2
On-line CPU(s) list: 0,1
CPU family:          6
Model name:          Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz
CPU MHz:             2394.259
NUMA node0 CPU(s):   0,1
Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology cpuid tsc_known_freq pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm cpuid_fault invpcid_single pti fsgsbase bmi1 avx2 smep bmi2 erms invpcid xsaveopt
[root@ip-172-31-41-190 jenkins]# vim config.xml 
[root@ip-172-31-41-190 jenkins]# systemctl daemon-reload 
[root@ip-172-31-41-190 jenkins]# systemctl restart jenkins
[root@ip-172-31-41-190 jenkins]# systemctl status jenkins
● jenkins.service - Jenkins Continuous Integration Server

```


