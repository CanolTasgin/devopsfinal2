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
                    docker.withRegistry('https://registry.hub.docker.com', env.DOCKER_CREDS) {
                        def appImage = docker.build(env.DOCKER_IMAGE)
                        appImage.push()
                    }
                }
            }
        }
    }
}
