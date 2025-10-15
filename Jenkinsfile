@Library('sample-pipeline-shared-library') _

pipeline {
   agent {
    // First, select the node
    label 'my-linux-agent'
    // Then, specify the container to run on that node
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
        stage('Deploy to Production') {
    steps {
        input(message: 'Proceed with deployment to production?')
        
        // If you click 'Proceed', the steps below will run
        sh 'echo "Deploying to production..."'
    }
}
        stage('Build and Archive') {
            steps {
                executeMavenBuild()
            }
        }
    }
}
