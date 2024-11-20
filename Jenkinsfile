pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                // Pull the code from the GitHub repository
                git url: 'https://github.com/mayurpupankar/Square_Root_Calculator.git', branch: 'main'
            }
        }

        stage('Setup Python Environment') {
            steps {
                // Install dependencies
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests using pytest
                sh './venv/bin/pytest > test-results.txt'
            }

            post {
                always {
                    // Archive test results
                    archiveArtifacts artifacts: 'test-results.txt', allowEmptyArchive: true
                    junit 'test-results.txt'
                }
            }
        }

        stage('Code Quality Check') {
            steps {
                // Run code quality checks (using pylint as an example)
                sh './venv/bin/pylint square_root_calculator.py > pylint-report.txt'
            }

            post {
                always {
                    // Archive pylint report
                    archiveArtifacts artifacts: 'pylint-report.txt', allowEmptyArchive: true
                }
            }
        }

        stage('Deploy to Test Environment') {
            steps {
                // Here, deploy your code to a test environment (for example, a Docker container)
                echo 'Deploying to test environment...'
            }
        }
    }

    post {
        success {
            echo 'Build and tests completed successfully!'
        }
        failure {
            echo 'Build or tests failed. Check the logs for more details.'
        }
    }
}
