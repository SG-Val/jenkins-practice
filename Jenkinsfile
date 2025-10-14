@Library('sample-pipeline-shared-library') _

pipeline {
    agent {
        docker { 
            image 'maven:3-jdk-11' 
        }
    }

    parameters {
        string(name: 'MESSAGE', defaultValue: 'Hello', description: 'The message to print')
    }

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Test Library') {
            steps {
                greetUser('Sundar')
            }
        }
        stage('Run Tests in Parallel') {
            steps {
                parallel (
                    "Unit Tests": {
                        echo "Running Unit Tests..." // Steps for unit tests would go here
                    },
                    "Integration Tests": {
                        echo "Running Integration Tests..." // Steps for integration tests would go here
                    }
                )
            }
        }
        stage('Build and Archive') {
            steps {
                executeMavenBuild()
            }
        }
    }
}
