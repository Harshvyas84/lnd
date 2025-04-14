// Declarative Pipeline syntax
pipeline {
    // **CHANGE 1: Define the agent as a Docker container**
    // This tells Jenkins to run the steps inside a container
    // based on the official golang image, version 1.21
    agent {
        docker {
            image 'golang:1.21' 
            // Optional: Mount the workspace inside the container
            // args '-v $WORKSPACE:$WORKSPACE -w $WORKSPACE' 
        }
    }

    // Define build stages
    stages {
        stage('Checkout') {
            // **CHANGE 2: Checkout happens automatically with docker agent**
            // So we remove the explicit 'checkout scm' step here
            // But keep the deleteDir for cleanliness
            steps {
               script {
                   echo "Workspace: ${env.WORKSPACE}"
                   // Clean workspace before checkout (happens implicitly now)
                   // deleteDir() // Not strictly needed now, checkout is clean
               }
            }
        }

        stage('Setup Go') {
            steps {
                // Go is now pre-installed in the golang:1.21 image
                // We just verify the version
                sh 'go version' 
                sh 'go env GOROOT GOPATH' // See where Go is setup
            }
        }

        stage('Run Go Tests') {
            steps {
                // Run basic Go unit tests
                // This should now FIND the 'go' command
                sh 'go test ./...' 
            }
        }
    }

    // Optional: Define actions to always run after the build
    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
