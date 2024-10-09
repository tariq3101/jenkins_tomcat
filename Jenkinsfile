pipeline {
    agent any
    
    tools {
        jdk 'JDK 21'
        maven 'maven_build'
    }
    
    environment {
        // Define environment variables for Tomcat
        WAR_FILE = 'target/java-tomcat-maven-example.war' // Path to the generated WAR file (use forward slashes)
        TOMCAT_URL = 'http://localhost:7080' // Tomcat server URL
        TOMCAT_USER = 'Tariq' // Tomcat Manager username
        TOMCAT_PASSWORD = 'tariq123' // Tomcat Manager password
    }
    
    stages {
        stage('Clean Project') {
            steps {
                sh "mvn clean"
            }
        }

        stage('Build Project') {
            steps {
                sh "mvn package"
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
		    //in this case it will be C:\ProgramData\Jenkins\.jenkins\workspace\war-deploy-jenkins-tomcat
                    def warFilePath = "${WORKSPACE}/${WAR_FILE}" // Use forward slashes in path
                    echo "WAR file path: ${warFilePath}"
                    
                    // Check if the WAR file exists before deploying
                    if (fileExists(warFilePath)) {
                        echo 'WAR file found, proceeding with deployment...'
                        
                        // Deploy the WAR file to Tomcat using curl and Tomcat Manager API
                        sh """
                            curl --upload-file "${warFilePath}" \
                            --user ${TOMCAT_USER}:${TOMCAT_PASSWORD} \
                            "${TOMCAT_URL}/manager/text/deploy?path=/roshambo&update=true"
                        """
                    } else {
                        error('WAR file not found! Build might have failed.')
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Build completed'
        }
    }
}
