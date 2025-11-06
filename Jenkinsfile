pipeline {
    agent any

    tools {
        maven 'MAVEN_3'
        jdk 'JDK_17'
    }

    environment {
        PROJECT_NAME = "java-maven-webapp"
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo "Cloning source code..."
                git branch: 'main',
                    url: 'https://github.com/<username>/<repo>.git'
            }
        }

        stage('Build') {
            steps {
                echo "Running Maven Build..."
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running Test Cases..."
                sh 'mvn test'
            }
        }

        stage('Package JAR/WAR') {
            steps {
                echo "Packaging Application..."
                sh 'mvn package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
                    echo "WAR/JAR file archived successfully!"
                }
            }
        }

    }

    post {
        success {
            echo "✅ CI Pipeline Completed Successfully!"
        }
        failure {
            echo "❌ Build Failed!"
        }
    }
}

