pipeline {
    agent any

    stages {
        stage('Verify') {
            steps {
                echo 'Jenkins read the nginx-site project'
            }
        }

        stage('Build image') {
            steps {
                sh 'docker build -t meri-website:ci .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKERHUB_USER',
                    passwordVariable: 'DOCKERHUB_TOKEN'
                )]) {
                    sh '''
                        set +x
                        printf '%s' "$DOCKERHUB_TOKEN" | docker login --username "$DOCKERHUB_USER" --password-stdin
                        docker tag meri-website:ci "$DOCKERHUB_USER/meri-website:ci"
                        docker push "$DOCKERHUB_USER/meri-website:ci"
                        docker logout
                    '''
                }
            }
        }
    }
}
