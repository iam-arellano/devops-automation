pipeline {
    agent any
    tools{
        maven 'maven3'
    }
    stages{
        stage('Git Checkout ') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/iam-arellano/devops-automation'
            }
        }

        stage('Build Maven'){
            steps{
               sh 'mvn clean install'
            }
        }

                stage('Docker Build & Push') {
            steps {
                   script {
                 
                            withDockerRegistry(credentialsId: 'jenkins-docker-credentials') {
                            sh "docker build -t devops-automation ."
                            sh "docker tag devops-automation raemondarellano/devops-automation:latest"
                            sh "docker push raemondarellano/devops-automation:latest "
                        }
                   } 
            }
        }
        

    }
}