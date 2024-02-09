pipeline {
    agent any

    stages {
        stage('connecting k8') {
            steps {
                sh 'kubectl config use-context arn:aws:eks:us-west-2:844609451572:cluster/devops-eks-KEKg5KnX'
            }
        }
      
      stage('helm install') {
            steps {
                sh 'helm upgrade --install reactjs $WORKSPACE --values $WORKSPACE/values.yaml'
            }
        }
      stage('pods status') {
            steps {
                sh 'kubectl get pods'
            }
      }
        
    }
}
