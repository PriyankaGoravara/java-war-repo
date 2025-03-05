pipeline {
    agent { label 'slave' } 
    environment {
        AWS_REGION = 'ap-south-1' 
        ECR_REPO = '203918867107.dkr.ecr.ap-south-1.amazonaws.com/my-ecr-repo'
        IMAGE_NAME = 'java1-app-image'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/PriyankaGoravara/java-war-repo.git'
            }
        }

        stage('Build Java Application') {
            steps {
                sh 'mvn clean package -DskipTests' 
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "sudo docker build -t $IMAGE_NAME ."
            }
        }

        stage('Push Image to AWS ECR') {
            steps {
                script {
                    
                    sh """
                    aws ecr get-login-password --region $AWS_REGION | sudo docker login --username AWS --password-stdin $ECR_REPO
                    """

                
                    sh "sudo docker tag $IMAGE_NAME:latest $ECR_REPO:latest"

              
                    sh "sudo docker push $ECR_REPO:latest"
                }
            }
        }
    }
}
