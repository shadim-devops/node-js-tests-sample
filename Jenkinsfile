pipeline {
    agent any

    environment {
        VERSION = "1.0"
        ENVIRONMENT = "dev"
        AUTHOR = "Dmytro"
        EMAIL = "email@example.com"
    }

    stages {

        stage('Checkout') {
            steps {
                script {
                    try {
                        echo "Downloading code..."
                        git url: 'https://github.com/shadim-devops/node-js-tests-sample.git', branch: 'main'
                    } catch (e) {
                        echo "Checkout failed: ${e}"
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        echo "Building version ${env.VERSION}"
                        sh 'echo "Build done"'
                    } catch (e) {
                        echo "Build failed: ${e}"
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        echo "Running tests..."
                        sh 'echo "Tests passed"'
                    } catch (e) {
                        echo "Tests failed: ${e}"
                        currentBuild.result = 'UNSTABLE'
                    }
                }
            }
        }

        stage('Deploy') {
            when {
                expression {
                    return currentBuild.result == null || currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                script {
                    try {
                        echo "Deploying to ${env.ENVIRONMENT}"
                        sh 'echo "Deploy done"'
                    } catch (e) {
                        echo "Deploy failed: ${e}"
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                def duration = currentBuild.durationString
                echo "Pipeline finished in ${duration}"
            }
        }

        success {
            echo "Pipeline succeeded"
            mail to: "${env.EMAIL}",
                 subject: "SUCCESS: Pipeline completed",
                 body: """Pipeline SUCCESS

Author: ${env.AUTHOR}
Version: ${env.VERSION}
Environment: ${env.ENVIRONMENT}
Time: ${currentBuild.durationString}
Result: SUCCESS
"""
        }

        failure {
            echo "Pipeline failed"
            mail to: "${env.EMAIL}",
                 subject: "FAILED: Pipeline error",
                 body: """Pipeline FAILED

Author: ${env.AUTHOR}
Version: ${env.VERSION}
Environment: ${env.ENVIRONMENT}
Time: ${currentBuild.durationString}
Result: FAILURE
"""
        }
    }
}
