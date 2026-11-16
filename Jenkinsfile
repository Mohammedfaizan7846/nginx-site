pipeline {
    agent any
    stages {
        stage('Verify') {
            steps {
                echo 'Jenkins successfully read the nginx-site project working on it'
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -t meri-website:ci .'
            }
        }
    }
}

