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
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}