pipeline {
    agent any

    environment {
        DEPLOY_PATH = "/var/www/html/index.html"
    }

    stages {
       stage('Checkout') {
    steps {
        git(
            branch: 'main',
            url: 'git@github.com:zubair-tc/JenkinsTask.git',
            credentialsId: 'JENKINS_USER_SSH_KEY' 
        )
    }
}

        stage('Lint HTML') {
            steps {
                script {
                    sh 'htmlhint basic.html'
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh 'echo "Deploying HTML to Apache..."'
                sh "sudo cp basic.html $DEPLOY_PATH"  // Double quotes for variable expansion
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build failed. Fix linting or deployment issue.'
        }
    }
}
