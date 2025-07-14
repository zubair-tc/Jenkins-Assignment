pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/zubair-tc/JenkinsTask.git'
      }
    }

    stage('Deploy with Apache') {
      steps {
        script {
          sh '''
mkdir -p deploy
cp basic.html deploy/

cat <<EOF > deploy/Dockerfile
FROM httpd:alpine
COPY basic.html /usr/local/apache2/htdocs/index.html
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
