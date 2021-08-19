pipeline {
    agent any
    environment {
        DOCKER_TAG = "v1"
    }
    stages {
        stage('Clonado repo Git') {
            steps {
                git credentialsId: 'GitHubCred',
                url: 'https://github.com/enmanuelmoreira/Go-JWT-Postgres-Mysql-Restful-API'
            }
        }
        stage('Construyendo app') {
            steps {
                sh "docker build . -f Dockerfile.gotest"
            }
        }
        stage('Probando app') {
            steps {
                sh "docker-compose -f docker-compose.test.yml up --build --abort-on-container-exit"
            }
        }
    }
    //     stage('Push a DockerHub') {
    //         steps {
    //             withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPassword')]) {
    //                 sh "docker login -u enmanuelmoreira -p ${dockerHubPassword}"
    //             }

    //             sh "docker push enmanuelmoreira/go-restful-api-demo:${DOCKER_TAG}"
    //         }
    //     }
    //     stage('Desplegando app') {
    //         steps {
    //             ansiblePlaybook colorized: true,
    //                             credentialsId: 'web',
    //                             disableHostKeyChecking: true,
    //                             extras: "-e DOCKER_TAG=${DOCKER_TAG}",
    //                             installation: 'ansible',
    //                             inventory: 'inventory',
    //                             playbook: 'deploy.yml'
    //         }    
    //     }
    // }
}


docker-compose -f docker-compose.test.yml up --build --abort-on-container-exit