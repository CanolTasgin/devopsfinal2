pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "canolt/devopsfinal:latest"
        DOCKER_CREDS = "devops-final-docker-username-password"
        GITHUB_CREDS = "devops-final-git-token"
    }

    stages {
        stage('Build') {
            steps {
                git branch: 'master',  credentialsId: env.GITHUB_CREDS, url: 'https://github.com/CanolTasgin/devopsfinal2.git'
                script {
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_CREDS, passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "echo '$DOCKER_PASSWORD' | docker login -u $DOCKER_USERNAME --password-stdin https://index.docker.io/v1/"
                        def appImage = docker.build(env.DOCKER_IMAGE)
                        appImage.push()
                    }
                }
            }
        }
    }
}
