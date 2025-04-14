// Declarative Pipeline syntax
pipeline {
    // Run on any available agent (the built-in Jenkins node in this case)
    agent any

    // Define build stages
    stages {
        stage('Checkout') {
            steps {
                // Check out code from version control (defaults to the repo linked to the pipeline)
                script {
                    // Clean workspace before checkout
                    deleteDir() 
                }
                checkout scm 
                script {
                    // Print current branch (for debugging)
                    echo "Checked out branch: ${env.BRANCH_NAME}" 
                }
            }
        }

        stage('Setup Go') {
            steps {
                // Using a Tool installer is the Jenkins way, but requires setup.
                // For simplicity here, we assume Go is available on the agent.
                // In a real setup, use Tools -> Global Tool Configuration -> Go
                // Or use a Docker agent with Go pre-installed.
                // We'll just check the version assuming it exists.
                sh 'go version' 
            }
        }

        stage('Run Go Tests') {
            steps {
                // Run basic Go unit tests
                // Similar to GitHub Actions, 'make check' would need bitcoind
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
