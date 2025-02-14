pipeline { 
    agent any 
    stages { 
        stage('Clean Up') { 
            steps { 
                cleanWs() 
            } 
        } 
        stage('Clone') { 
            steps { 
                checkout scm 
            } 
        } 
        stage('Build & Test in Parallel') { 
            parallel { 
                stage('Build') { 
                    steps { 
                        sh 'mvn clean install -DskipTests' 
                    } 
                } 
                stage('Test') { 
                    steps { 
                        sh 'mvn test' 
                    } 
                } 
            } 
        } 
    } 
}
