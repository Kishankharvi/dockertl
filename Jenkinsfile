pipeline {
  agent any

  environment {
    IMAGE_NAME = "kishankharvi/jenkins-cicd"
    IMAGE_TAG  = "${BUILD_NUMBER}"
  }

  stages {
    stage('Checkout') {
      steps {
	git 'https://github.com/Kishankharvi/dockertl.git'
      }
    }

    stage('Build Image') {
      steps {
        sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
      }
    }

    stage('Push Image') {
      steps {
        sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
      }
    }

    stage('Deploy') {
      steps {
        sh """
          docker stop app || true
          docker rm app || true
          docker run -d -p 3000:3000 \
            --name app ${IMAGE_NAME}:${IMAGE_TAG}
        """
      }
    }
  }
}
