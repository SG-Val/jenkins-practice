pipeline {
    agent any

    parameters {
        string(name: 'MESSAGE', defaultValue: 'Hello', description: 'The message to print')
    }

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
                // We access the parameter using params.MESSAGE
                echo "The user-provided message is: ${params.MESSAGE}"
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
