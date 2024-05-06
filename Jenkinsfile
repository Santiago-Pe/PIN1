pipeline {
    agent any

    environment {
        DOCKER_HOST = 'tcp://host.docker.internal:2375'  // Use host.docker.internal to refer to the Docker daemon on the host
    }

    stages {
        stage('Building image') {
            steps {
                sh 'docker build -t testapp .'
            }
        }

        stage('Run tests') {
            steps {
                sh 'docker run testapp npm test'
            }
        }

        stage('Deploy Image') {
            steps {
                sh '''
                docker tag testapp 127.0.0.1:5000/mguazzardo/testapp
                docker push 127.0.0.1:5000/mguazzardo/testapp
                '''
            }
        }
    }
}
