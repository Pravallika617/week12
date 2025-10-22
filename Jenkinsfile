pipeline {
    agent any 
    stages {
      stage('Build Docker Image'){
        steps{
          echo "Build Docker Image"
          bat "docker build -t kubdemoapp:v1"
        }
      }
      stage('Docker Login'){
        steps{
          bat 'docker login -u pravallikas029 -p password'
        }
      }
      stage('push Docker Image to Docker Hub'){
        steps{
          echo "push Docker Image to Docker Hub"
          bat "docker tag kuberdemoapp:v1 pravallikas029/sample:kubeimage1"

          bat "docker push pravallikas029/sample:kubeimage1"
        }
      }
      stage('Deploy to Kubernetes'){
        steps{
            // apply deployment & service
            bat 'kubectl apply -f deployment.yaml --validate=false'
            bat 'kubectl apply -f service.yaml'
        }
      }
      post{
        success{
            echo 'Build,test,run and jar creation successful and artifact is ready!'
        }
        failure{
            echo 'Build or test failure'
        }
    }
}
