node {
    docker.image('maven:3.8.6-openjdk-11-slim').inside {
        stage('Check Workspace') {
            sh 'pwd && ls -al'
        }

        // stage('Build') {
        //     sh 'cd /home/Documents/submission_ci_jenkins/simple-java-maven-app && mvn clean install'
        // }

        // stage('Test') {
        //     sh 'cd /home/Documents/submission_ci_jenkins/simple-java-maven-app && mvn test'
        // }
    }
}