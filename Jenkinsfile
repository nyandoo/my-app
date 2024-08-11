pipeline {
    agent {
        label 'agent'
    }
    environment {
        MY_KUBECONFIG = credentials('my-kubeconfig')
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
                withCredentials([usernamePassword(credentialsId: 'ab2fd322-fb8e-41ba-928b-e454b89f28a5', passwordVariable: 'password', usernameVariable: 'username')]) 
                    {   
                        sh "docker login -u ${username} -p ${password}"
                        sh 'docker push my-app:latest' 
                    }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh("kubectl --kubeconfig $MY_KUBECONFIG get pods")
                    // kubernetesDeploy(configs: "k8s/deployment.yaml", "k8s/service.yaml")
                }
            }
        }
    }
}
