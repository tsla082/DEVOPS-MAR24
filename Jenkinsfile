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
