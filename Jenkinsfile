pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/zubair-tc/JenkinsTask.git'
      }
    }

    stage('Deploy to Apache (host)') {
      steps {
        script {
          sh '''
            sudo cp basic.html /var/www/html/index.html
          '''
        }
      }
    }
  }
}
