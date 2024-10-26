pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9' // Ensure this matches the Maven configuration in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                // Cloning the Git repository
                git 'https://github.com/muthu512/hello.git'
            }
        }
        stage('Build') {
            steps {
                // Running Maven build to generate the JAR file
                bat 'mvn clean package'
            }
        }
        stage('Deploy') {
    steps {
        script {
            // Define the correct source path for the JAR file
            def jarSource = "${WORKSPACE}\\target\\spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar"
            
            // Define the static deployment folder
            def deployFolder = "C:\\Users\\Dell-Lap\\Downloads\\Newfolder"
            
            // Create the deployment folder (if it doesn't already exist)
            bat "mkdir ${deployFolder}"
            
            // Copy the JAR file to the target folder
            bat "copy ${jarSource} ${deployFolder}"
            
            // Run the Spring Boot application from the specific folder on port 1010
            bat "start java -jar ${deployFolder}\\spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar --server.port=1010"
        }
    }
}

                }
            }
        }
    }
}
