pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = 'dockerhub-credentials'      // Jenkins credentials ID
    DOCKERHUB_USERNAME = 'syedghouse21'                       // Your Docker Hub username
    IMAGE_NAME = 'docker-demo'                           // Your image name
    IMAGE_TAG = 'v1'                                      // Your image tag
  }

  stages {
    stage('Checkout Code') {
      steps {
        echo 'Checking out code...'
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          echo "Building Docker image..."
          sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
        }
      }
    }

    stage('Tag Docker Image') {
      steps {
        script {
          echo "Tagging Docker image..."
          sh "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${DOCKERHUB_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG}"
        }
      }
    }

    stage('Push Docker Image to Docker Hub') {
      steps {
        withCredentials([usernamePassword(credentialsId: "${DOCKERHUB_CREDENTIALS}", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          script {
            echo "Logging in to Docker Hub..."
            sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
            echo "Pushing image to Docker Hub..."
            sh "docker push ${DOCKERHUB_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG}"
          }
        }
      }
    }
  }

  post {
    success {
      echo 'Docker image built and pushed successfully!'
    }
    failure {
      echo 'Pipeline failed.'
    }
  }
}
