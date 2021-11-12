pipeline {
stages {
stage('Clone Git repository') {
checkout scm
}

stage('Build Image') {
sh 'echo Build application image'
app = docker.build("donalpatino/hello-world", "./Dockerfile.build")
}

stage('Push image to Docker Hub') {
sh 'echo Push image to a Docker Hub'
docker.withRegistry('https://registry.hub.docker.com', 'docker_id') {
app.push("latest") 
}
}

stage('Run container') {
sh 'echo Run container'
sh 'ansible-playbook /opt/playbooks/docker_playbook.yaml -i /opt/playbooks/hosts'
}
}
}