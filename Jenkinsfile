pipeline {
    agent {
        docker {
            image 'node:18.17.1-alpine3.18' 
            args '-p 3000:3000' 
        }
    }
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh "chmod +x -R ${env.WORKSPACE}"
                sh './scripts/test.sh'
            }
        }
         stage('Deliver') {
            steps {
                echo "Delivering.."
                sh "chmod +x -R ${env.WORKSPACE}"
                sh './scripts/deliver.sh'
                // input message: 'Finished using the web site? (Click "Proceed" to continue)'
                // sh './scripts/kill.sh'
            }
        }
    }
}