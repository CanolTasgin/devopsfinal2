pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "canolt/devopsfinal:latest"
        DOCKER_CREDS = "ea83fe5e-7591-4043-b145-934600bf6bc1"
        GITHUB_CREDS = "devops-final-git-token"
    }

    stages {
        stage('Build') {
            steps {
                git branch: 'master',  credentialsId: env.GITHUB_CREDS, url: 'https://github.com/CanolTasgin/devopsfinal2.git'
                script {
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_CREDS, passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "echo '$DOCKER_PASSWORD' | docker login -u $DOCKER_USERNAME --password-stdin https://registry.hub.docker.com"
                        def appImage = docker.build(env.DOCKER_IMAGE)
                        appImage.push()
                    }
                }
            }
        }
    }
}
