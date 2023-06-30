# cloud4c_jenkinsb1

## Revision 

<img src="rev.png">

### User & RBAC 

<img src="user.png">

# IMportant searching role in given link  -- https://plugins.jenkins.io/

[click_here](https://plugins.jenkins.io/)

### Notification in jenkins 

<img src="alert.png">

### smtp 

<img src="smtp.png">

## jenkinsfile 

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
        // checking keys 
        stage('checking private key in source code'){
            steps {
                echo 'we are using trufflehog tool to detect'
                sh 'docker run --rm  trufflesecurity/trufflehog:latest github --repo https://github.com/redashu/ashu-cisco-webUI.git --json  >keycheck.txt'
                sh 'cat  keycheck.txt' 
            }
        }
        // dockerpipeline to build docker image 
        stage('building image using docker pipeline'){
            steps {
                echo 'using docker pipeline to build image'
                script {
                    def imageName = "dockerashu/ashuweb"
                    def imageTag  = "sec-check$BUIlD_NUMBER"
                    // calling build function
                    docker.build(imageName + ":" + imageTag, "-f Dockerfile .")
                }
                // verify image build
                sh 'docker images | grep dockerashu'
            }
        }
        // creating container using compose 
        stage('creating container and testing health page'){
            steps {
                echo 'running compose'
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
                sh 'docker-compose ps'
                // access page which mean container got created successfully 
                sh 'curl -f http://localhost:1990/health.html'
            }
        }
        // docker pipeline to push image to docker hub 
        stage('pushing image to docker hub'){
            steps {
                echo 'using docker pipeline plugin to push '
                script {
                    def imageName = "dockerashu/ashuweb"
                    def imageTag  = "sec-check$BUIlD_NUMBER"
                    def imageCred = "a7a29583-59b1-4391-a492-313c05498ea3"
                    docker.withRegistry('https://registry.hub.docker.com',imageCred){
                        docker.image(imageName + ":" + imageTag).push()
                    }
                }
            }
        }
        // creating deployment using above image
        stage('creating deployment and verify it'){
            steps {
                echo 'cloning git repo for yaml purpose'
                git 'https://github.com/redashu/cloud4c-jenkins-cd.git'
                sh 'ls'
                // lets apply yaml files
                sh 'kubectl apply -f https://raw.githubusercontent.com/redashu/cloud4c-jenkins-cd/master/ns.yaml'
                sh 'kubectl apply -f https://raw.githubusercontent.com/redashu/cloud4c-jenkins-cd/master/deploy.yaml'
                // check deployment 
                sh 'kubectl -n ashu-final-app get deploy | grep -i ashu'
                sh 'sleep 10'
                sh 'kubectl -n ashu-final-app get pod | grep -i running'
            }  
        }
        stage('creating service and ingress'){
            steps {
                echo 'creating service'
                sh 'kubectl apply -f https://raw.githubusercontent.com/redashu/cloud4c-jenkins-cd/master/service.yaml'
                sh 'sleep 3'
                sh 'kubectl apply -f  https://raw.githubusercontent.com/redashu/cloud4c-jenkins-cd/master/ingress.yaml'
                // checking 
                sh 'kubectl get svc,ing -n ashu-final-app'
            }
        }
     
    }
}

```
