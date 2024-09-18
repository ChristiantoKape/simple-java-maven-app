node {
    stage('Checkout') {
        checkout scm
    }

    docker.image('maven:3.9.2-openjdk-17-slim').inside {
        stage('Build') {
            sh 'mvn clean install'
        }

        stage('Test') {
            sh 'mvn test'
        }
    }
}