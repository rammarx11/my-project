pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Iam-mithran/kuber.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t newimage /var/lib/jenkins/workspace/kuber'
                sh 'sudo docker tag newimage iammithran/newimage:latest'
                sh 'sudo docker tag newimage iammithran/newimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push iammithran/newimage:latest'
                sh 'sudo docker image push iammithran/newimage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo helm lint /var/lib/jenkins/workspace/project/hello-world'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
                sh 'sudo helm install /var/lib/jenkins/workspace/project/hello-world/ --dry-run --generate-name'
                sh 'sudo helm install /var/lib/jenkins/workspace/project/hello-world/ --generate-name'////
                
                
            }
        }
    }
}
