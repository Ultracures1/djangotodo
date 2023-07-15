pipeline {
    agent any
    stages {
        stage('code') {
            steps {
                echo "clone the code  "
                git url: "https://github.com/Ultracures1/djangotodo.git" , branch : "develop"
            
            }
        }
        stage('build') {
            steps {
                echo "Build the ource code"
                sh "docker build -t myap ."
            }
        }
        stage ('push'){
            steps {
                echo "push the code to dockerhub"

                withCredentials([ usernamePassword(credentialsId: 'sn88', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                sh "docker tag myapp ${env.dockerHubUser}/myapp:v1"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                sh "docker push ${env.dockerHubUser}/myapp:v1  "
                }
                
            }
            
        }
        
        stage('Deploy') {
            steps {
                echo "deploy"
                sh "docker run -d -p 8000:8000 myapp"  
                
            }
        }
    }
}
