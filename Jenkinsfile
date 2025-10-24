pipeline {
    agent any
    environment {
        SONAR_HOST_URL = 'https://sonarcloud.io/' // Replace with your SonarQube server URL
         SONAR_HOST_URL_CREDENTIALS = 'sonarqube' // Replace with your SonarQube token credentials ID
        
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
            environment {
                SCANNER_HOME = tool 'Sonarqube'
            }   
             steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''${SCANNER_HOME}/bin/sonar-scanner \
                    -Dsonar.organization=Viralpatel489 \
                    -Dsonar.projectName=sprinbootjavaapp \
                    -Dsonar.projectKey=springbootjavaapp \
                    -Dsonar.java.binaries=.
                  '''
                }
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
                echo 'Deploying1....'
            }
        }
    }
}