pipeline {
    agent any
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
                echo 'sonarQubeScan..'
                 withSonarQubeEnv('sonarqube') {
                    sh 'mvn sonar:sonar'}
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