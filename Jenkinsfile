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
            sh 'apk add --no-cache openssh-client'
            sshagent(credentials: ['ec2-ssh-key']) {
                sh """
                    ssh -o StrictHostKeyChecking=no ec2-user@ec2-54-253-207-230.ap-southeast-2.compute.amazonaws.com "
                    sudo yum install -y nginx
                    sudo systemctl start nginx
                    sudo systemctl enable nginx
                    sudo mkdir -p /var/www/html
                    sudo chown ec2-user:ec2-user /var/www/html
                    "
                    scp target/my-app-1.0-SNAPSHOT.jar ec2-user@ec2-54-253-207-230.ap-southeast-2.compute.amazonaws.com:/var/www/html/
                """
            }
            sleep(time: 1, unit: 'MINUTES')
            sh './jenkins/scripts/deliver.sh'
        }
    }
}
