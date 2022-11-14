pipeline {
    agent {
        docker {
            image 'kennethreitz/pipenv:latest'
            args '-u root --privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('test') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'master']], userRemoteConfigs: [[url: 'https://github.com/rbenavente']]])
                script { 
                    sh """export PRISMA_API_URL=https://api.eu.prismacloud.io
                    pipenv install
                    pipenv run pip install bridgecrew
                    pipenv run bridgecrew --directory . --bc-api-key ${ACCESS_KEY}::${SECRET_KEY} --repo-id github.com/rbenavente"""
                }
            }
        }
    }

}
