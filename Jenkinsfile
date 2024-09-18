node {
    def mvnHome = tool 'M3'
    
    stage('Build') {
        sh "${mvnHome}/bin/mvn -B clean package"
    }
    
    stage('Test') {
        sh "${mvnHome}/bin/mvn test"
    }
}