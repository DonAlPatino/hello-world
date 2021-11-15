pipeline {
  environment {
    registry = "gustavoapolinario/docker-test"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }

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
dockerImage = docker.build("donalpatino/hello-world -f ./Dockerfile.build")
        }
    }
}

stage('Push image to Docker Hub') {
    steps {
        script {
sh 'echo Push image to a Docker Hub'
docker.withRegistry('https://registry.hub.docker.com', 'docker_id') {
dockerImage.push("latest")
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