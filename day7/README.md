# cloud4c_jenkinsb1

### building java based webapp into .war using maven 

### installing maven in one of the jenkins slave node

```
 24  yum install java-11-openjdk-devel.x86_64  java-11-openjdk.x86_64
   25  jps
   26  yum search maven 
   27  yum install maven

```

### jenkins file with maven 

```
pipeline {
    // choosing particular slave
    agent {
        label 'slave1'
    }

    stages {
        stage('cloning java webapp from git repo') {
            steps {
                echo 'taking source code ..'
                // using inbuild keyword git 
                git 'https://github.com/redashu/java-springboot.git'
                // verify 
                sh 'ls'
            }
        }
        stage('building this project using apache maven'){
            steps {
                echo 'Lets use apache maven to build java webapp to .war'
                // building now
                sh 'mvn clean package'
                // verification 
                sh 'ls ; ls target'
            }
        }
    }
    post {
        success {
            echo 'hey we have done it with maven also'
        }
        failure {
            echo 'we need to figure out what happened'
        }
    }
}

```
