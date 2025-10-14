pipeline {
    agent any

    parameters {
        string(name: 'MESSAGE', defaultValue: 'Hello', description: 'The message to print')
    }
// A small change to trigger polling
    triggers {
        // Poll for changes every two minutes
        pollSCM('H/2 * * * *')
    }

    tools {
        maven 'Maven-3.9.11'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Set the build description using the environment variable
                    currentBuild.description = "Commit: ${env.GIT_COMMIT}"
                }
                echo "Now building commit: ${env.GIT_COMMIT}"
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
