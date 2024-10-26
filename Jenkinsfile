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

<<<<<<< HEAD:Jenkinsfile.txt
                    // Copy the JAR to the deployment folder
                    bat "copy /Y \"${buildJar}\" \"${deployJar}\""

                    // Run the JAR file
                    bat "java -jar \"${deployJar}\""
=======
                    // Copy the JAR to the specified deployment folder
                    bat "copy /Y \"${buildJar}\" \"${deployJar}\""

                    // Run the JAR directly from the deployment folder with the specified port
                    bat "java -jar \"${deployJar}\" --server.port=1010"
>>>>>>> ad28a9776c51f9c953b291994f73dd496f9b359e:Jenkinsfile
                }
            }
        }

        stage('Post-Deployment Verification') {
            steps {
<<<<<<< HEAD:Jenkinsfile.txt
                echo 'Running tests...'
                // You can add custom verification logic here
                // Example: HTTP check to verify the application is running
                // def response = bat(script: 'curl -s -o /dev/null -w "%{http_code}" http://localhost:2020', returnStdout: true)
                // if (response.trim() == '200') {
                //     echo 'Application is up and running!'
                // } else {
                //     error('Application did not start successfully!')
                // }
=======
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
>>>>>>> ad28a9776c51f9c953b291994f73dd496f9b359e:Jenkinsfile
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
