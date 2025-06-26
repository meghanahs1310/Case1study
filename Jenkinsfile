pipeline {
    agent any

    tools {
        maven 'Maven 3' // Match Global Tool Configuration
    }

    // environment {
    //     SONARQUBE = 'SonarQube' // Match name in Jenkins config
    //     KUBECONFIG_CRED = 'KubeconfigId'  // Match name in Jenkins config
    // }

    stages {
        stage('Checkout from SCM') {
            steps {
                git branch:'dev', url: 'https://github.com/meghanahs1310/Case1study.git'
            }
        }
    
        stage('Build Application') {
            steps {
                sh 'mvn clean install'
            }
        }
        
   //      stage('SonarQube Analysis') {
   //          steps {
   //              withSonarQubeEnv("${SONARQUBE}") {
   //                  sh 'mvn sonar:sonar'
   //              }
   //          }
   //      }
            
   //      stage ('QualityGate') {
   //              steps {
   //              waitForQualityGate abortPipeline: true, credentialsId: 'SonarId'
   //              }
   //          }
        
   //       stage('Build - Scan - Push Docker Image') {
   //            steps {
   //              script {
   //                      withDockerRegistry(credentialsId: 'DockerId') {
   //                      sh 'docker build -t demo-app-name:latest -f Dockerfile .'
   //                      sh 'trivy image --severity CRITICAL --exit-code 1 demo-app-name:latest'
   //                      sh 'docker tag demo-app-name:latest marutih8/demo-app-name'
   //                      sh 'docker push marutih8/demo-app-name'
   //                  }
   //              }
   //          }
   //      }
        
   //        stage('Deploy to Kubernetes') {
   //          steps {
   //            withAWS(credentials: 'AWS_Credentials', region: 'us-east-1') {
   //              withCredentials([
   //              file(credentialsId: 'KubeconfigId', variable: 'KUBECONFIG')
   //            ]) {
   //              sh '''
   //                  export KUBECONFIG=$KUBECONFIG
   //                  kubectl apply -f deployment.yaml
   //                  kubectl apply -f service.yaml
   //              '''
   //             }
   //            }
   //          }
   //        }
   //         stage('Deploy to dev') {
   //          steps {
   //            withAWS(credentials: 'AWS_Credentials', region: 'us-east-1') {
   //              withCredentials([
   //              file(credentialsId: 'KubeconfigId', variable: 'KUBECONFIG')
   //            ]) {
   //              sh '''
   //                  export KUBECONFIG=$KUBECONFIG
   //                  kubectl apply -f deployment.yaml --namespace=dev
   //                  kubectl apply -f service.yaml --namespace=dev
   //              '''
   //             }
   //            }
   //          }
   //        }
   //         stage('Deploy to qa') {
   //          steps {
   //            withAWS(credentials: 'AWS_Credentials', region: 'us-east-1') {
   //              withCredentials([
   //              file(credentialsId: 'KubeconfigId', variable: 'KUBECONFIG')
   //            ]) {
   //              sh '''
   //                  export KUBECONFIG=$KUBECONFIG
   //                  kubectl apply -f deployment.yaml --namespace=qa
   //                  kubectl apply -f service.yaml --namespace=qa
   //              '''
   //             }
   //            }
   //          }
   //        }
          
   //    stage('Approval to Deploy to Prod') {
   //      steps {
   //        script {
   //          input(
   //           message: "Approve deployment to Prod?", 
   //          parameters: [
   //            booleanParam(name: 'Proceed', defaultValue: false, description: 'Approve the deployment to Prod')
   //          ]
   //        )
   //      }
   //    }
   //  }
   //  stage('Deploy to Prod') {
   //    when {
   //      expression { return params.Proceed == true }
   //    }
   //      steps {
   //          withAWS(credentials: 'AWS_Credentials', region: 'us-east-1') {
   //          withCredentials([file(credentialsId: 'KubeconfigId', variable: 'KUBECONFIG')]) {
   //              sh '''
   //                  export KUBECONFIG=$KUBECONFIG
   //                  kubectl apply -f deployment.yaml --namespace=prod
   //                  kubectl apply -f service.yaml --namespace=prod
   //              '''
   //                }
   //              }
   //            }
   //          }
   //        }
          
   // post {
   //  success {
   //      echo 'Deployment successful!'
   //      mail to: 'marutihundekar55@gmail.com',
   //           subject: "✅ Jenkins Pipeline Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
   //           body: "Good news! Jenkins job '${env.JOB_NAME}' (build #${env.BUILD_NUMBER}) succeeded.\n\nCheck details at: ${env.BUILD_URL}"
   //  }

   //  failure {
   //      echo 'Deployment failed!'
   //      mail to: 'marutihundekar55@gmail.com',
   //           subject: "❌ Jenkins Pipeline Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
   //           body: "Oops! Jenkins job '${env.JOB_NAME}' (build #${env.BUILD_NUMBER}) failed.\n\nCheck logs at: ${env.BUILD_URL}"
   //  }
  }
}
