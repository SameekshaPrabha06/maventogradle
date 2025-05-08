pipeline {
    agent any

    tools {
        gradle 'Gradle'    // Use the exact name defined in Jenkins
        jdk 'JDK'          // Use the exact name defined in Jenkins
    }

    environment {
        JAR_FILE = 'build/libs/MyMavenToGradle-1.0-SNAPSHOT.jar'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build with Gradle') {
            steps {
                echo 'Building with Gradle...'
                sh 'gradle clean build'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'gradle test'
            }
        }

        stage('Run JAR') {
            steps {
                sh "java -jar ${env.JAR_FILE}"
            }
        }
    }

    post {
        success {
            echo "✅ Success!"
        }
        failure {
            echo "❌ Failure!"
        }
    }
}

