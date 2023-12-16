pipeline {

    agent any

    tools {
        maven 'maven'
        ansible 'ansible'
    }

    stages {
        stage('Build code with maven') {
            steps {
                sh 'mvn --version'
                sh 'java --version'
                sh 'mvn clean package -Dmaven.test.failure.ignore=true'
            }
        }
        stage('Test Ansible'){
            steps {
                sh 'ansible -i host -m ping all'
            }
        }

        stage('Pushing image') {
            steps{
                withDockerRegistry(credentialsId:'dockerhub', url:'') {
                sh 'docker build -t phdg1410/spring:v1 .'
                sh 'docker push phdg1410/spring'
            }

            }
            
            
        }
    }
}