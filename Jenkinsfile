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
/*
pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
               git branch: 'master', url:'https://github.com/Stywar/devops-dotnet-account-23'
            }
        }
        
       stage('Builder Image') {
            steps {
             // aqui hacer el docker login
             bat(script: 'docker login --username antony0618 --password Fvc1231988' , returnStdout:true); 
             bat(script: 'docker build -t antony0618/ms-account .' , returnStdout:true); 
             bat(script: 'docker push  antony0618/ms-account' , returnStdout:true);  
            }
        }
        
         
        stage ("Deploy AKS") {
           steps {
            bat(script: 'az login --service-principal --username 60445a5a-4c7d-404e-96a0-0d5c83c4978f --password 9N38Q~OKV.zjd1UvnHzq6hxdJd~tGhNc3NqgxbVo --tenant 74343d69-5375-4c7a-8cc9-08986488c964', returnStdout: true);
            bat(script: 'az account set --subscription "Developer"', returnStdout: true);
            bat(script: 'az aks get-credentials --resource-group Devops --name polyglot-cluster-azure & kubectl config get-contexts --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
            bat(script: 'kubectl config use-context polyglot-cluster-azure --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
            bat(script: 'kubectl apply -f k8s.yml --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
            bat(script: 'kubectl rollout restart deployment app-deployment --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
           }
       }
    }
}
*/
