pipeline {
  agent any
  environment {
    GITHUB_TOKEN=credentials('github-token')
    IMAGE_NAME='darinpope/jenkins-example-ghcr'
    IMAGE_VERSION='8.5-204'
  }
  stages {
    stage('cleanup') {
      steps {
        bat 'echo docker system prune -a --volumes --force'
      }
    }
    stage('build image') {
      steps {
        bat 'echo docker build -t $IMAGE_NAME:$IMAGE_VERSION .'
      }
    }
    stage('login to GHCR') {
      steps {
        bat 'echo $GITHUB_TOKEN_PSW | docker login ghcr.io -u $GITHUB_TOKEN_USR --password-stdin'
      }
    }
    stage('tag image') {
      steps {
        bat 'echo docker tag $IMAGE_NAME:$IMAGE_VERSION ghcr.io/$IMAGE_NAME:$IMAGE_VERSION'
      }
    }
    stage('push image') {
      steps {
        bat 'echo docker push ghcr.io/$IMAGE_NAME:$IMAGE_VERSION'
      }
    }
  }
  post {
    always {
      bat 'docker logout'
    }
  }
}
