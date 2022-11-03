pipeline {
    agent any
    stages {
        stage('Fetching Code') {
            steps {
                
                git 'https://github.com/mustafasaber36/python-app-cicd.git'
                sh 'pwd'
                sh 'ls'
            }
        }
        
        stage('Building Artifact'){
            steps{
               
                withCredentials([usernamePassword(credentialsId: 'dockerhubsecrets', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
                
                
                sh '''
                    docker build . -f ~/workspace/'python pipeline'/python-app/Dockerfile -t moustafasaber36/app:python
                    docker login -u ${USERNAME} -p ${PASSWORD}
                    docker push moustafasaber36/app:python
                '''
                }
            }   
        }

        stage('Deploying'){
            steps{
                    sh 'pwd'
                    sh 'ls'
                    sh 'kubectl apply -f ~/workspace/"python pipeline"/kubernetes/redis.yml'
                    sh 'kubectl apply -f ~/workspace/"python pipeline"/kubernetes/backend-servcie.yml' 
                    sh 'kubectl apply -f ~/workspace/"python pipeline"/kubernetes/project-python.yml'
                    sh 'kubectl apply -f ~/workspace/"python pipeline"/kubernetes/frontend-service.yml'
                    sh 'kubectl get svc'
             }
           }
    }
}
