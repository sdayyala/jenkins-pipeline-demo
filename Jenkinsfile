node {
    def mvnHome = tool 'maven3'
    
    try {
        // stage('Checkout') {
        //     checkout scm
        // }

        stage('Checkout') {
            git branch: 'main',
                credentialsId: 'gitcreds',
                url: 'https://github.com/sdayyala/jenkins-pipeline-demo.git'
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