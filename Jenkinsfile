node {
    def mvnHome = tool 'maven3'
    
    try {
        stage('Checkout') {
            checkout scm
        }

        stage('Build & Test') {
            sh "${mvnHome}/bin/mvn clean install"
        }

        stage('Archive') {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
    catch (exc) {
        echo "Pipeline failed: ${exc}"
        throw exc
    }
}