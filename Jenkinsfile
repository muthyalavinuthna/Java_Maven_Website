pipeline {
    agent any
    stages {

        stage('Checkout') {
            steps {
		checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '4009e931-ec7b-46fc-87fb-36c528f1c27a', url: 'https://github.com/muthyalavinuthna/Java_Maven_Website.git']])
                
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t food-webapp .'
            }
        }

        stage('Docker Run') {
            steps {
                sh 'docker rm -f food-container || true'
                sh 'docker run -d -p 4045:8080 --name food-container food-webapp'
            }
        }
    }
}
