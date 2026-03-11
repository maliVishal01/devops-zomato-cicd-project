pipeline {

agent any

stages {

stage('Clone Repository') {
steps {
git 'https://github.com/YOUR_USERNAME/devops-zomato-clone.git'
}
}

stage('Build Docker Image') {
steps {
sh 'docker build -t zomato-clone .'
}
}

stage('Security Scan') {
steps {
sh 'trivy image zomato-clone'
}
}

stage('Deploy Application') {
steps {
sh 'docker rm -f zomato || true'
sh 'docker run -d -p 80:80 --name zomato zomato-clone'
}
}

}

}
