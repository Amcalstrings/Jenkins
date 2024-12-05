pipeline{
    agent any
    tools{
        maven 'maven3'
    }

    stages{
        stage('Checkout code'){
            steps{
                checkout scm
            }
        }

        stage('Build java application'){
            steps{
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build docker image'){
            steps{
                sh 'docker build -t amcal/my-java-app:v1'
            }
        }

        stage('Push docker image'){
            steps{
                withCredentials([string(credentialsId: 'DOCKER_LOGIN', url: '')]){
                    sh 'docker push -t amcal/my-java-app:v1'
                }
            }
        }
    }
}