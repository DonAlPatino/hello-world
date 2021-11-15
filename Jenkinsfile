pipeline {
    agent any
stages {
stage('Clone Git repository') {
    steps {
checkout scm
    }
}

stage('Build Image') {
    steps {
        script {
sh 'echo Build application image'
def app = docker.build("hello-world", "./Dockerfile.build")
        }
    }
}

stage('Push image to Docker Hub') {
    steps {
        script {
sh 'echo Push image to a Docker Hub'
docker.withRegistry('https://registry.hub.docker.com', 'docker_id') {
app.push("latest")
}
} 
}
}

stage('Run container') {
steps {
sh 'echo Run container'
sh 'ansible-playbook /opt/playbooks/docker_playbook.yaml -i /opt/playbooks/hosts'
}
}
}
}