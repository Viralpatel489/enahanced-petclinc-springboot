pipeline {
    agent any
    tools {
        maven 'maven'
    }
    environment{
        IMAGE_NAME = 'springbootapp'
        IMAGE_TAG = 'latest'
        TENANT_ID ='ec78375d-0db0-42cf-82a6-2e6403e95936'
        ACR_NAME = 'springbootdockerreg'
        ACR_LOGIN_SERVER = 'springbootdockerreg.azurecr.io'
        FULL_IMAGE_NAME = "${ACR_LOGIN_SERVER}/${IMAGE_NAME}:${IMAGE_TAG}"
        RG              = "socgen"
        NAME            = "myAKSCluster"
    }
    stages {
        stage('Checkout FROM GIT') {
            steps {
                git branch: 'prod' , url: 'https://github.com/Viralpatel489/enahanced-petclinc-springboot.git'
        }
      }
        stage('Validate with Maven ') {
            steps {
                sh 'mvn validate'
            }
        }
        stage('Compile with Maven ') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Sonar Analysis ') {
            // environment {
            //     SCANNER_HOME = tool 'sonarproject2'
            // }   
            steps {
                withCredentials([string(credentialsId: 'token1', variable: 'SONAR_AUTH_TOKEN')]) {
                withSonarQubeEnv('sonarqubeserver') {
                    sh '''${SCANNER_HOME}/bin/sonar-scanner \
                    -Dsonar.organization=viralpatel489 \
                    -Dsonar.projectName=project2 \
                    -Dsonar.projectKey=viralpatel489_project2 \
                    -Dsonar.sources=. \
                    -Dsonar.java.binaries=. \
                    -Dsonar.token=${SONAR_AUTH_TOKEN}
                  '''
                    }
                }
            }         
        }
        //  stage('Maven Package ') {
        //     steps {
        //         sh 'mvn package'
        //     }
        // }
        // stage('Sonar Quality Gate') {
        //     steps {
        //         timeout(time: 1, unit: 'MINUTES') {
        //             waitForQualityGate abortPipeline: true, credentialsId: 'sonar'
        //         }
        //     }
        // }
        // stage('Docker Build') {
        //     steps {
        //         script {
        //             echo "Building Docker Image......."
        //             docker.build ("${IMAGE_NAME}:${IMAGE_TAG}") 
        //         }
        //     }
        // }
        // stage('Azure Login TO ACR') {
        //     steps {
        //         withCredentials([usernamePassword(credentialsId: 'azure-acr-spn', usernameVariable: 'AZURE_USERNAME', passwordVariable: 'AZURE_PASSWORD')]) {
        //             script {
        //                 echo "Azure Login Started"
        //                 sh '''
        //                 az login --service-principal -u $AZURE_USERNAME -p $AZURE_PASSWORD --tenant $TENANT_ID
        //                 az acr login --name $ACR_NAME
        //                 '''
        //             }
        //         }
        //     }
        // }
        // stage('Docker Push to ACR') {
        //     steps {
        //         script {
        //             echo "Docker Image Push to ACR"
        //             sh '''
        //             docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${FULL_IMAGE_NAME}
                   
        //             docker push ${FULL_IMAGE_NAME}
        //             '''
        //         }
        //     }
        // }
        // stage('Azure Login TO AKS') {
        //     steps {
        //         withCredentials([usernamePassword(credentialsId: 'azure-acr-spn', usernameVariable: 'AZURE_USERNAME', passwordVariable: 'AZURE_PASSWORD')]) {
        //             script {
        //                 echo "Azure Login to AKS"
        //                 sh '''
        //                 az login --service-principal -u $AZURE_USERNAME -p $AZURE_PASSWORD --tenant $TENANT_ID
        //                 az aks get-credentials --resource-group $RG --name $NAME --overwrite-existing
        //                 '''
        //             }
        //         }
        //     }
        // }
        // stage('Deploy to AKS') {
        //     steps {
        //         withCredentials([usernamePassword(credentialsId: 'azure-acr-spn', usernameVariable: 'AZURE_USERNAME', passwordVariable: 'AZURE_PASSWORD')]) {
        //             script {
        //                 echo "Azure Login to AKS"
        //                 sh '''
        //                 az login --service-principal -u $AZURE_USERNAME -p $AZURE_PASSWORD --tenant $TENANT_ID
        //                 kubectl apply -f k8s/sprinboot-deployment.yaml
        //                 '''
        //             }
        //         }
        //     }
        // }
    }
}



































// pipeline {
//     agent any
//     environment {
//         SONAR_HOST_URL = 'https://sonarcloud.io/' // Replace with your SonarQube server URL
//         SONAR_HOST_URL_CREDENTIALS = 'sonarqube' // Replace with your SonarQube token credentials ID
//         SONAR_ORG_KEY = 'viralpatel489' // Replace with your SonarQube organization key
//         SONAR_PROJECT_KEY = 'sprinbootjavaapp' // Replace with your SonarQube project key
    
        
//     }
//     tools {
//         maven 'maven'
//     }
//     stages {
//         stage('Checkout & clean') {
//             steps {
//                 echo 'Checking out code...'
//                 git url: 'https://github.com/Viralpatel489/enahanced-petclinc-springboot.git', branch: 'prod'
                
//                 echo 'Cleaning workspace...'
//                 sh 'mvn clean'
//             }
//         }
//         stage('sonarQubeScan') {
//             steps {
//             withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_TOKEN')]){
//             sh "mvn verify sonar:sonar \
//             -Dsonar.organization=${env.SONAR_ORG_KEY} \
//             -Dsonar.projectKey=${env.SONAR_PROJECT_KEY} \
//             -Dsonar.host.url=${env.SONAR_HOST_URL} \
//             -Dsonar.login=${env.SONAR_HOST_URL_CREDENTIALS}"
//                 }
//             }
//         }
        
//         // stage('Test') {
//         //     steps {
//         //         echo 'Testing..'
//         //         sh 'mvn test'
//         //     }
//         // }
//         // stage('build') {
//         //     steps {
//         //         echo 'Deploying12....'
//         //     }
//         // }
//     }
// }