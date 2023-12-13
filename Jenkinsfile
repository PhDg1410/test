pipeline {

    agent any

    tools {
        maven 'maven'
    }

    stages {
        stage('Build code with maven') {
            steps {
                sh 'mvn --version'
                sh 'java --version'
                sh 'mvn clean package -Dmaven.test.failure.ignore=true'
            }
        }

        stage('Pushing image') {
            steps{
                withDockerRegistry(credentialsId:'dockerhub', url:'https://hub.docker.com/repositories/phdg1410/spring') {
                sh 'docker build -t springboot .'
                sh 'docker push springboot'
            }

            }
            
            post {
        // Clean after build
                always {
                    cleanWs()
            }
    }
        }
    }
}