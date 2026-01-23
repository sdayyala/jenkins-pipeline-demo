node('rhel') {
    
    def mvnHome = tool 'maven3'

    stage('Checkout') {
        echo 'Checking out source code'
        git branch: 'main',
            credentialsId: 'gitcreds',
            url: 'https://github.com/sdayyala/jenkins-pipeline-dec-scripted.git'
    }

    stage('Build') {
        echo 'Running Maven build'
        sh "${mvnHome}/bin/mvn clean compile"
    }

    stage('Test') {
        echo 'Running Maven tests'
        sh "${mvnHome}/bin/mvn test"
    }

    stage('Package') {
        echo 'Packaging artifact'
        sh "${mvnHome}/bin/mvn package"
    }

    stage('Archive') {
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
    }
}
