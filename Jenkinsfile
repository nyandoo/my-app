pipeline {
    agent {
        label 'manager'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('my-app')
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/', 'nyando7') {
                        docker.image('my-app').push('latest')
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    kubernetesDeploy(configs: 'k8s/deployment.yaml', kubeconfigId: 'kube-config')
                }
            }
        }
    }
}