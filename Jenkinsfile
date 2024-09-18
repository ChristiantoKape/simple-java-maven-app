node {
    docker.image('maven:3.8.6-openjdk-11-slim').inside {
        stage('Build') {
            sh 'mvn clean install'
        }

        stage('Test') {
            sh 'mvn test'
        }
    }
}