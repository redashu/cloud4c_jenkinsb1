# cloud4c_jenkinsb1

### Revision 

<img src="rev.png">

### jenkinsfile more info 

<img src="more.png">

## sample jenkins file

```
pipeline {
    agent any

    stages {
        stage('taking souce code from github') {
            steps {
                echo 'Hello World we are starting with github code'
                // lets use git option to clone data from repo 
                git 'https://github.com/redashu/ashu-cisco-webUI.git'
                // my slave nodes are linux so we use sh incase of windows we use bat
                sh 'ls '
                sh  'java -version'
            }
        }
        stage('checking docker connection'){
            steps {
                // using docker version 
                echo 'running docker command !..'
                sh 'docker version'
            }
        }
    }
}

```
