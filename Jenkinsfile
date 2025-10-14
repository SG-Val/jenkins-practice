@Library('sample-pipeline-shared-library') _
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
        stage('Test Library') {
            steps {
                greetUser('Sundar')
            }
        }
        stage('Build and Archive') {
            steps {
                executeMavenBuild()
            }
        }
    }
    
}
