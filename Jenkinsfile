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
                withDockerRegistry(credentialsId:'dockerhub', url:'https://hub.docker.com/') {
                sh 'docker build -t phdg1410/spring .'
                sh 'docker push phdg1410/spring'
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