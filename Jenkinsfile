pipeline {
  agent any
  environment {
    IMAGE_NAME = "meghanahs/case1"
    MANIFEST_PATH = "manifest_file/k8s"
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/meghanahs1310/Case1study.git'
      }
    }

    stage('Build and Test') {
      steps {
        sh 'ls -ltr'
        sh 'mvn clean package'
      }
    }

  //   stage('Build and Push Docker Image') {
  //     steps {
  //       script {
  //         sh "docker build -t ${IMAGE_NAME} ."
  //       }
  //     }
  //   }

  //   stage('Push to DockerHub') {
  //     steps {
  //       withCredentials([usernamePassword(credentialsId: 'DOCKERHUB_CREDENTIALS', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
  //         sh '''
  //           echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
  //           docker push $IMAGE_NAME
  //         '''
  //       }
  //     }
  //   }

  //   stage('Static Code Analysis') {
  //     environment {
  //       SONAR_URL = "http://13.127.80.68:9000/"
  //     }
  //     steps {
  //       withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_AUTH_TOKEN')]) {
  //         sh """
  //           mvn sonar:sonar \
  //             -Dsonar.login=$SONAR_AUTH_TOKEN \
  //             -Dsonar.host.url=$SONAR_URL
  //         """
  //       }
  //     }
  //   }

  //   stage('Deploy to Dev') {
  //     steps {
  //       script {
  //         sh """
  //           kubectl apply -f ${MANIFEST_PATH}/dev/deployment.yaml --namespace=dev
  //         """
  //       }
  //     }
  //   }

  //   stage('Deploy to Test') {
  //     steps {
  //       script {
  //         sh """
  //           kubectl apply -f ${MANIFEST_PATH}/test/deployment.yaml --namespace=test
  //           kubectl rollout status deployment/case1 --namespace=test
  //         """
  //       }
  //     }
  //   }

  //   stage('Approval to Deploy to Prod') {
  //     steps {
  //       script {
  //         input(
  //           message: "Approve deployment to Prod?", 
  //           parameters: [
  //             booleanParam(name: 'Proceed', defaultValue: false, description: 'Approve the deployment to Prod')
  //           ]
  //         )
  //       }
  //     }
  //   }

  //   stage('Deploy to Prod') {
  //     when {
  //       expression { return params.Proceed == true }
  //     }
  //     steps {
  //       script {
  //         sh """
  //           kubectl apply -f ${MANIFEST_PATH}/prod/deployment.yaml --namespace=prod
  //           kubectl rollout status deployment/case1 --namespace=prod
  //         """
  //       }
  //     }
  //   }
  // }

  // post {
  //   success {
  //     echo 'Deployment successful!'
  //     mail to: 'bhavanijd51@gmail.com',
  //          subject: "Jenkins Pipeline Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
  //          body: "Good news! Jenkins job '${env.JOB_NAME}' (build #${env.BUILD_NUMBER}) completed successfully.\n\nCheck details: ${env.BUILD_URL}"
  //   }

  //   failure {
  //     echo 'Deployment failed!'
  //     mail to: 'bhavanijd51@gmail.com',
  //          subject: "Jenkins Pipeline Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
  //          body: "Oops! Jenkins job '${env.JOB_NAME}' (build #${env.BUILD_NUMBER}) failed.\n\nCheck details: ${env.BUILD_URL}"
  //   }
  }
}
