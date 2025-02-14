pipeline {
    agent { label 'Maven-slave-label' }
    
    stages {
        stage('Clone') {
            steps {
                sh 'git clone https://github.com/PriyankaGoravara/java-war-repo.git'
            }
        }

        stage('Build') {
            steps {
                dir('java-war-repo') { 
                    sh 'mvn clean install'
                }
            }
        }
        stage('Test') {
            steps {
                dir('java-war-repo') {  
                    sh 'mvn test'
                }
            }
        }
    }
}
