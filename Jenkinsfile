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
                echo "STARTING Unit Tests..."
                sh 'sleep 5'
                echo "ENDING Unit Tests."
            },
            "Integration Tests": {
                echo "STARTING Integration Tests..."
                sh 'sleep 5'
                echo "ENDING Integration Tests."
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
