node('rhel') {

    def startTime = System.currentTimeMillis() 
    def mvnHome = tool 'maven3'

    try {

        stage('Checkout') {
            git branch: 'main',
                credentialsId: 'gitcreds',
                url: 'https://github.com/sdayyala/jenkins-pipeline-demo.git'
        }

        stage('Build') {
            sh "${mvnHome}/bin/mvn clean compile"
        }

        stage('Test') {
            sh "${mvnHome}/bin/mvn test"
        }

        stage('Package') {
            sh "${mvnHome}/bin/mvn package"
        }

        stage('Archive') {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }

        def endTime = System.currentTimeMillis()
        def duration = (endTime - startTime) / 1000

        echo "🎉 Scripted pipeline executed successfully in ${duration} seconds"

    } catch (err) {

        def endTime = System.currentTimeMillis()
        def duration = (endTime - startTime) / 1000

        echo "❌ Scripted pipeline failed after ${duration} seconds"
        throw err
    }
}
