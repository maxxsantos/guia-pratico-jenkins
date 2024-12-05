pipeline {
    agent any

    stages {
        stage('build docker image') {
            steps {
                sh "docker build -f ./src/Dockerfile -t maxxsantos/guia-jenkins:${env.BUILD_ID} ./src"
                // script {
                //     dockerapp = docker.build("maxxsantos/guia-jenkins:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                // }
            }
        }
        stage('Docker login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "dockerhub", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo -n ${DOCKER_PASS} | docker login --username ${DOCKER_USER} --password-stdin docker.io"
                        // sh "docker login -u ${DOCKER_USER} --password-stdin DOCKER_PASS https://registry.hub.docker.com"
                    }
                }
            }
        }
        stage('push docker image') {
            steps {
                script {
                    sh 'echo "Executando push docker image"'
                    sh "docker push maxxsantos/guia-jenkins:${env.BUILD_ID}"
                    // docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    //     dockerapp.push('latest')
                    //     dockerapp.push("${env.BUILD_ID}")
                    // }
                }
            }
        }
        stage('Cleanup') {
            echo 'Limpando as imagens locais...'
            sh "docker rmi maxxsantos/guia-jenkins:${env.BUILD_ID} || true"
        }
        stage('Deploy') {
            steps {
                sh 'echo "Executando o docker build"'
            }
        }
    }
}