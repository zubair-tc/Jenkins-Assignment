pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/<your-username>/<your-repo>.git'
      }
    }

    stage('Deploy with Apache') {
      steps {
        script {
          sh '''
            mkdir -p deploy
            cp index.html deploy/
            cat <<EOF > deploy/Dockerfile
            FROM httpd:alpine
            COPY index.html /usr/local/apache2/htdocs/
            EOF

            cd deploy
            docker build -t html-site .
            docker stop html-container || true
            docker rm html-container || true
            docker run -d --name html-container -p 8081:80 --network jenkins-net html-site
          '''
        }
      }
    }
  }
}
