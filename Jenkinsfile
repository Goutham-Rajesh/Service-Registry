pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Goutham-Rajesh/Service-Registry.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {
                bat "docker rm -f Service-container"
                bat "docker rm -f Service-image"
                bat "docker build -t Service-image ."
                bat "docker run -p 8761:8761 -d --name Service-container Service-image"
            }
        }
    }
}
