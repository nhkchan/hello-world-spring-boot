pipeline {
    agent any

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
    }
    
    post {
        success {
            withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                sh "docker push nhkchan/springtestdocker:${env.BUILD_ID}"
                sh "docker push nhkchan/springtestdocker:latest"
            }
        }
    }
}
