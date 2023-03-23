pipeline {
  agent any
  environment {
    GITHUB_TOKEN=credentials('github-token')
    IMAGE_NAME='https://dockerhub/hello-world'
    IMAGE_VERSION='nanoserver-1809'
  }
  stages {
    stage('cleanup') {
      steps {
        bat'docker system prune -a --volumes --force'
      }
    }
    stage('build image') {
      steps {
        bat 'echo docker build -t $IMAGE_NAME:$IMAGE_VERSION .'
      }
    }
    stage('login to GHCR') {
      steps {
        bat 'echo echo $GITHUB_TOKEN_PSW | docker login ghcr.io -u $GITHUB_TOKEN_USR --password-stdin'
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
