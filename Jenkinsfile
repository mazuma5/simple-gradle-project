//author: Avik mazumderss
pipeline {
    agent any
    tools {
        gradle 'gradle5.2.1'
        jdk 'java1.8.0'
    }
    stages {
        stage('Build') {
            steps {
                sh 'gradle clean war'
            }
        }
        stage('Test') {
            steps {
                sh 'gradle test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Upload') {
            steps {
                sh 'curl -X PUT -u admin:password -T target/my-app-1.0-SNAPSHOT.jar "http://localhost:8081/artifactory/libs-release-local/my-app-1.0-SNAPSHOT.jar"'
            }
        }
        stage('Deploy') {
            steps {
                sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
            }
        }
    }
}
