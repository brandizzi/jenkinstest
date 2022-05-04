pipeline {
    agent { any { image 'maven:3.8.4-openjdk-11-slim' } }
    stages {
        stage('build') {
            steps {
                sh 'mvn test'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'target/**/*.class', fingerprint: true
            junit 'target/surefire-reports/**/*.xml'
        }
    }
}
