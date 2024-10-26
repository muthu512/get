pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git url: 'https://github.com/muthu512/get.git', branch: 'master', credentialsId: 'muthu512'
            }
        }

        stage('Build') {
            steps {
                // Build the project using Maven
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                // Run tests using Maven
                bat 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Define paths for the build JAR and the deployment folder
                    def buildJar = "C:\\Users\\Dell-Lap\\.jenkins\\workspace\\DeploySpringBoot\\target\\spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar"
                    def deployFolder = "C:\\Users\\Dell-Lap\\Downloads\\Newfolder"
                    def deployJar = "${deployFolder}\\spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar"

                    // Copy the JAR to the deployment folder
                    bat "copy /Y \"${buildJar}\" \"${deployJar}\""

                    // Check if port 1010 is already in use
                    def isPortInUse = bat(script: 'netstat -aon | findstr :1010', returnStatus: true) == 0
                    if (isPortInUse) {
                        error('Port 1010 is already in use. Please free it up before deployment.')
                    }

                    // Run the JAR directly from the deployment folder with the specified port
                    bat "java -jar \"${deployJar}\" --server.port=1010"
                }
            }
        }

        stage('Post-Deployment Verification') {
            steps {
                script {
                    echo 'Running tests...'
                    // Verification logic (HTTP check on the correct port)
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
