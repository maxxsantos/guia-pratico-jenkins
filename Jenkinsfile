pipeline {
    agent any

    stages {
        stage('build docker image') {
            steps {
                sh "docker build -f ./src/Dockerfile -t maxxsantos/guia-jenkins:${env.BUILD_ID} ./src"
                // script {
                //     dockerapp = docker.build("maxxsantos/guia-jenkins:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }
        stage('push docker image') {
            steps {
                script {
                    sh 'echo "Executando push docker image"'
                    // docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    //     dockerapp.push('latest')
                    //     dockerapp.push("${env.BUILD_ID}")
                    // }
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo "Executando o docker build"'
            }
        }
    }
}