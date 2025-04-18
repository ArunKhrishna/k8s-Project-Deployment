pipeline {
    agent any

    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/ArunKhrishna/k8s-Project-Deployment.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t arunk8simage /var/lib/jenkins/workspace/k8s_build_apr18'
                sh 'sudo docker tag arunk8simage arunkhrishna/arunk8simage:latest'
                sh 'sudo docker tag arunk8simage arunkhrishna/arunk8simage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push arunkhrishna/arunk8simage:latest'
                sh 'sudo docker image push arunkhrishna/arunk8simage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/k8s_build_apr18/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
