pipeline {
    agent any
    
    stages {
        stage('Checkout the repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Restore application') {
            steps {
                bat 'dotnet restore'
            }
        }
        
        stage('Build project') {
            steps {
                bat 'dotnet build'
            }
        }
        
        stage('Test running') {
            steps {
                bat 'dotnet test'
            }
            post {
                always {
                    // Publish test results if using MSTest, NUnit, or xUnit
                    publishTestResults testResultsFormat: 'VSTest', testResultsFiles: '**/*.trx'
                }
            }
        }
    }
    
    post {
        always {
            // Clean workspace after build
            cleanWs()
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
