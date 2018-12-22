pipeline {
    agent any

    tools {
        maven 'mvn-3.5.2'
    }
    
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Make Container') {
            steps {
                sh "docker build -t nhkchan/springtestdocker:${env.BUILD_ID} ."
                sh "docker tag nhkchan/springtestdocker:${env.BUILD_ID} nhkchan/springtestdocker:latest"
            }
        }
        stage('Run Docker Container') {
            steps {
                sh "docker run nhkchan/springtestdocker:latest"
            }
        }
    }
}
