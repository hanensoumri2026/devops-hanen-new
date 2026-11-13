pipeline {
    agent any

    tools {
        jdk 'jdk21'
        maven 'maven3'
    }

    stages {
        stage('1. Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('2. Build Backend (Maven)') {
            steps {
                dir('backend') {
                    bat 'mvn clean package -DskipTests'
                }
            }
        }

        stage('3. Test Backend') {
            steps {
                dir('backend') {
                   bat 'mvn test -DskipTests'
                }
            }
        }

        stage('4. Build Frontend (Angular)') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('5. Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'backend/target/*.jar', fingerprint: true
            }
        }
    }
}
