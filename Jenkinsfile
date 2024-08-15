pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('my-app')
                }
            }
        }
        stage('Deploy to Minikube') {
            steps {
                script {
                    // Push Docker image to Minikube's local Docker registry
                    //sh 'eval $(minikube -p minikube docker-env) && docker tag my-app my-app:latest'
                    
                    // Deploy to Kubernetes
                    //sh 'kubectl apply -f app/k8s/deployment.yaml --validate=false'
                    //sh 'kubectl apply -f app/k8s/service.yaml --validate=false'
                    sh 'kubectl set image deployment/my-app-deployment my-app=my-app:latest'
                }
            }
        }
    }
}

/*pipeline {
    agent {
        label 'agent'
    }
    environment {
        MY_KUBECONFIG = credentials('kube-config')
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
*/
