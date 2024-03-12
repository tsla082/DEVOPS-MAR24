pipeline {
    agent any
 
    stages {
        stage('SCM') {
            steps {
                git branch: 'master' , url: 'https://github.com/tsla082/devops-mar24'
            }
        }
        
        stage('Builder Image') {
            steps {
              bat(script: 'docker build -t khalios082/devops-mar24 .' ,returnStdout:true); 
              bat(script: 'docker push khalios082/devops-mar24' ,returnStdout:true); 
            }
        }
        stage('CD AKS'){
            steps {
                bat(script:'az login --service-principal --username 4dee3c5a-cd62-444b-b042-1080ad8cc7f8 --password GE88Q~uoWMRgGqcE4JrGyy2YmIfaYxZq-92oEdrY --tenant d82ed0c8-ae22-4264-b753-e10e9d437cd4',returnStdout:true);
                bat(script:'az account set --subscription fd29bf4d-fc8a-4eb7-8923-1623cd2f5c88', returnStdout:true);
                bat(script:'az aks get-credentials --resource-group devops --name DEVOPSMAR24 --overwrite-existing & kubectl config get-contexts --kubeconfig=C:/Users/LUISTORRES/.kube/config', returnStdout:true);
                bat(script:'kubectl config use-context DEVOPSMAR24  --kubeconfig=C:/Users/LUISTORRES/.kube/config', returnStdout:true);
                bat(script:'kubectl apply -f k8s.yml --kubeconfig=C:/Users/LUISTORRES/.kube/config', returnStdout:true);
                
            }
        }
    }
}
