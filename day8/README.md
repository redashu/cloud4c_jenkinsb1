# cloud4c_jenkinsb1

## Adding security feature in jenkins pipeline to scan static data like war file or docker image or github repo itself 

<img src="sec.png">

### store security check in a file -- which data can be used lator to analysse

```
pipeline {
    agent any

    stages {
        stage('taking webapp code from github URL') {
            steps {
                echo 'using git inbuild function to clone url'
                git 'https://github.com/redashu/ashu-cisco-webUI.git'
                // verify 
                sh 'ls | grep -i html'
            }
        }
        // lets do security check againts git repo before build
        stage('before build security scanning on the source code'){
            steps {
                echo 'doing security check'
                sh 'trivy repo https://github.com/redashu/ashu-cisco-webUI.git  >check1.txt'
                sh 'cat check1.txt'
                
            }
        }
    }
}

```
