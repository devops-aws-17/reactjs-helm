pipeline {
    agent any

    stages {
        stage('connecting k8') {
            steps {
                sh 'kubectl config use-context arn:aws:eks:us-west-2:844609451572:cluster/devops-eks-KEKg5KnX'
            }
        }
         stage('create namespace') {
            steps {
                sh 'kubectl create ns frontend'
            }
        }
         stage('creating secrets') {
            steps {
                sh '''
                kubectl create secret generic doker-cred \
                    --from-file=.dockerconfigjson=/home/ec2-user/.docker/config.json \
                    --type=kubernetes.io/dockerconfigjson
                '''
            }
        }
      
      stage('helm install') {
            steps {
                sh 'helm upgrade --install reactjs $WORKSPACE --values $WORKSPACE/values.yaml -n frontend'
            }
        }
      stage('pods status') {
            steps {
                sh 'kubectl get pods -n frontend'
            }
      }
        
    }
}
