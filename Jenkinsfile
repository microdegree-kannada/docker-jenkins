pipeline {
    environment {
    imagename = "518572/python-static"
    registryCredential = 'rajeev_docker_id'
    dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git([url: 'https://github.com/microdegree-kannada/docker-jenkins.git', branch: 'main'])

             }
        }
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build imagename 
                }
            }
        }
        stage('Deploy Image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("$BUILD_NUMBER")
                    dockerImage.push('latest')
                     }
                 }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $imagename:$BUILD_NUMBER"
                sh "docker rmi $imagename:latest"
            }
        }
    }
}


