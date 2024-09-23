node {
    docker.image('maven:3.9.2-eclipse-temurin-17-alpine').inside('-v /root/.m2:/root/.m2 --user root:root') {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }

        stage('Test') {
            checkout scm
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }

        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?'
        }

        stage('Deploy') {
            sleep(time: 1, unit: 'MINUTES')
            sh './jenkins/scripts/deliver.sh'
        }
    }
}
