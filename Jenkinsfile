pipeline {
    agent any
    stages {
        stage('Stage 2: Build & Push Docker Image') {
            steps {
                script {
                    echo "Building custom WordPress image from your fork..."
                    def customImage = docker.build("tahasalam/wordpress-sqe:${env.BUILD_NUMBER}")
                    
                    echo "Pushing to Docker Hub as official artifact..."
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        customImage.push()
                        customImage.push("latest")
                    }
                }
            }
        }
    }
    post {
        success {
            echo "Stage 2 COMPLETED SUCCESSFULLY!"
            echo "Your artifact is live at: https://hub.docker.com/r/tahasalam/wordpress-sqe"
        }
        failure {
            echo "Build failed — check logs"
        }
    }
}
