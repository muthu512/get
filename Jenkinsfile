pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/muthu512/get.git', branch: 'master', credentialsId: 'muthu512'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def buildJar = "C:\\Users\\Dell-Lap\\.jenkins\\workspace\\DeploySpringBoot\\target\\spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar"
                    def deployFolder = "C:\\Users\\Dell-Lap\\Downloads\\Newfolder"
                    def deployJar = "${deployFolder}\\spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar"

                    // Copy the JAR to the specified deployment folder
                    bat "copy /Y \"${buildJar}\" \"${deployJar}\""

                    // Run the JAR directly from the deployment folder with the specified port
                    bat "java -jar \"${deployJar}\" --server.port=1010"
                }
            }
        }

        stage('Post-Deployment Verification') {
            steps {
                script {
                    echo 'Running tests...'
                    // Example verification logic (HTTP check)
                    def response = bat(script: 'curl -s -o /dev/null -w "%{http_code}" http://localhost:1010', returnStdout: true)
                    if (response.trim() == '200') {
                        echo 'Application is up and running!'
                    } else {
                        error('Application did not start successfully!')
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
