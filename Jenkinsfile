pipeline {
    agent any

    tools {
        maven 'Maven-3.9.11'
    }

    stages {
        stage('Build') {
            steps {
                // This command will now run on the code in your repo
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
