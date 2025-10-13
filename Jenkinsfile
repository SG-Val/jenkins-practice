pipeline {
    agent any

    tools {
        maven 'Maven-3.9.11'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // We've added a specific commit hash to get an older version
                git url: 'https://github.com/jenkins-docs/simple-java-maven-app.git',
                    branch: '5f42775019a71550cdef48110b656b6c167d532b'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
    
    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
}
