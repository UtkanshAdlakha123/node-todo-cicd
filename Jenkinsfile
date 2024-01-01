pipeline{
    agent any
    
    stages{
        
        stage('Code')
        {
            steps{
                 git url: 'https://github.com/UtkanshAdlakha123/node-todo-cicd.git', branch : 'master'           
                 echo 'Clone the code from repo'
            }
        }
        
        stage('Build')
        {
            steps{
                sh 'docker build -t adlakhautkansh22/1stjan2ndimg .'
                echo 'build the image'
            }
        }
        
        stage('Push')
        {
            steps
            {
                script{
                    
                    withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKERHUB_TOKEN')]) {
                        
                        def dockerhubToken = env.DOCKERHUB_TOKEN
                        
                        // Login to Docker Hub using the access token
                        sh "echo ${dockerhubToken} | docker login -u adlakhautkansh22 --password-stdin"
                        
                        // Build and push your Docker image
        //                sh "docker build -t adlakhautkansh22/myhttpdimage ."
                        sh "docker push adlakhautkansh22/1stjan2ndimg"
                    }
                    
                }    
            }
        }
        
        stage('Deploy'){
        
            steps{
                sh 'docker-compose down'
                sh 'docker-compose up -d'
            }
        }
        
    }
}
