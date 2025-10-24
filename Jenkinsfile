pipeline {
    agent any
    environment {
        SONAR_HOST_URL = 'https://sonarcloud.io/' // Replace with your SonarQube server URL
        SONAR_HOST_URL_CREDENTIALS = 'sonarqube' // Replace with your SonarQube token credentials ID
        SONAR_ORG_KEY = 'viralpatel489' // Replace with your SonarQube organization key
        SONAR_PROJECT_KEY = 'sprinbootjavaapp' // Replace with your SonarQube project key
    
        
    }
    tools {
        maven 'maven'
    }
    stages {
        stage('Checkout & clean') {
            steps {
                echo 'Checking out code...'
                git url: 'https://github.com/Viralpatel489/enahanced-petclinc-springboot.git', branch: 'prod'
                
                echo 'Cleaning workspace...'
                sh 'mvn clean'
            }
        }
        stage('sonarQubeScan') {
            steps {
            sh "mvn verify sonar:sonar \
            -Dsonar.organization=${env.SONAR_ORG_KEY} \
            -Dsonar.projectKey=${env.SONAR_PROJECT_KEY} \
            -Dsonar.host.url=${env.SONAR_HOST_URL} \
            -Dsonar.login=${env.SONAR_HOST_URL_CREDENTIALS}"
            }
        }
        
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'mvn test'
            }
        }
        stage('build') {
            steps {
                echo 'Deploying12....'
            }
        }
    }
}