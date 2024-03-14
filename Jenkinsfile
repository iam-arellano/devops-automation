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
        stage('Push Docker image to Hub'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'jenkins-docker-credentials', toolName: 'docker-from-manage-tools')  {
                         sh "docker tag devops-automation raemond.arellano/devops-automation:latest"
                          sh "docker push raemond.arellano/devops-automation:latest "
                    }
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