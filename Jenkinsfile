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
        

        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t raemond.arellano/devops-automation .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'jenkins-docker-credentials', variable: 'jenkins-docker-credentials')]) {
                   sh 'docker login -u raemond.arellano -p ${jenkins-docker-credentials}'
                }
                   sh 'docker push raemond.arellano/devops-automation'
                }
            }
        }
        // stage('Deploy to k8s'){
        //     steps{
        //         script{
        //             kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
        //         }
        //     }
        // }
    }
}