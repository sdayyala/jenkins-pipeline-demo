pipeline {
    agent any

    tools {
        // Ensure 'maven-3.9.0' matches the name in Manage Jenkins -> Global Tool Configuration
        maven 'maven3'
    }

    stages {
        stage('Git-Checkout') {
            steps {
                git branch: 'main', 
                    credentialsId: 'gitcreds',
                    url: 'https://github.com/sdayyala/jenkins-pipeline-demo.git'
            }
        }

        stage('Maven-Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}