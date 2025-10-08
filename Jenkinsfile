pipeline{
    agent any
    stages{
        stage('Build Docker Image'){
            steps{
                echo "Build Docker image"
                bat "docker build -t kubdemoapp:v1 ."
            }
        }
        stage('Docker Login'){
            steps{
                bat 'docker login -u ppravalika -p Pravalika1709'
            }
        }
        stage('push docker image to Docker Hub'){
            steps{
                echo "push docker image to docker hub"
                bat "docker tag kubdemoapp:v1 ppravalika/week-8:kubeimage1"
                bat "docker push ppravalika/week-8:kubeimage1"
            }

        }
        stage('Deploy to kubernetes'){
            steps{
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
    post{
        success{
            echo 'Pipeline completed successfully'
        }
        failure{
            echo 'Pipeline failed.Please check the logs'
        }
    }
}
