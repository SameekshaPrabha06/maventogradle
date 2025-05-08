pipeline {
    agent any

    tools {
        gradle 'Gradle-8'     // Name configured in Jenkins Global Tool Config
        jdk 'JDK11'           // Name configured in Jenkins Global Tool Config
    }

    environment {
        JAR_FILE = 'build/libs/MyMavenToGradle-1.0-SNAPSHOT.jar'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm // Assumes you're using Git with Jenkins
            }
        }

        stage('Build with Gradle') {
            steps {
                echo 'Running gradle build...'
                sh 'gradle clean build'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'gradle test'
            }
        }

        stage('Verify Jar Output') {
            steps {
                echo 'Listing generated files...'
                sh 'ls -lh build/libs'
            }
        }

        stage('Run the Application') {
            steps {
                echo "Running ${env.JAR_FILE}"
                sh "java -jar ${env.JAR_FILE}"
            }
        }
    }

    post {
        success {
            echo "✅ Build completed and JAR executed successfully!"
        }
        failure {
            echo "❌ Build or execution failed!"
        }
    }
}

