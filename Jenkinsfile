
pipeline {
  agent any

  environment {
    IMAGE_NAME = "meghanahs/case1"
    MANIFEST_PATH = "manifest_file/k8s"
    KUBECONFIG = credentials('kubeconfig-file')
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
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh "docker build -t ${IMAGE_NAME} ."
      }
    }

    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker_cre', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
          sh """
            echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
            docker push ${IMAGE_NAME}
          """
        }
      }
    }

     stage('Static Code Analysis') {
       environment {
         SONAR_URL = "http://65.2.172.71:9000"
       }
       steps {
         withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_AUTH_TOKEN')]) {
           sh '''
             echo "Waiting for SonarQube to be ready..."
             until curl -s $SONAR_URL/api/system/status | grep -q '"status":"UP"'; do
               echo "SonarQube is not ready yet. Waiting 5 seconds..."
               sleep 5
             done

             echo "SonarQube is UP. Starting analysis..."
             mvn sonar:sonar \
               -Dsonar.login=$SONAR_AUTH_TOKEN \
               -Dsonar.host.url=$SONAR_URL
          '''
         }
    }
     }
    
    stage('Deploy to Dev') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'aws-creds', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
          sh 'kubectl apply -f ${MANIFEST_PATH}/dev/deployment.yaml --namespace=dev'
        }
      }
    }

    stage('Deploy to Test') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'aws-creds', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
          sh 'kubectl apply -f ${MANIFEST_PATH}/dev/deployment.yaml --namespace=test'
        }
      }
    }

       stage('Approval to Deploy to Prod') {
      steps {
        script {
          def userInput = input(
            message: "Approve deployment to Prod?",
            parameters: [
              booleanParam(name: 'Proceed', defaultValue: false, description: 'Approve the deployment to Prod')
            ]
          )
          // Save to environment so it can be used in next stage
          env.PROCEED_TO_PROD = userInput.toString()
        }
      }
    }

    stage('Deploy to Prod') {
      when {
        expression {
          return env.PROCEED_TO_PROD == 'true'
        }
      }
      steps {
        withCredentials([usernamePassword(credentialsId: 'aws-creds', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
          sh 'kubectl apply -f ${MANIFEST_PATH}/dev/deployment.yaml --namespace=prod'
        }
      }
    }
  }
}
