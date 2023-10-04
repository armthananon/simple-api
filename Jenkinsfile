pipeline {
    agent any

    stages {
        stage('Clone') {
            agent { label 'test' }
            steps {
                sh 'rm -f -r simple-api && git clone https://github.com/armthananon/simple-api'
            }
        }
        stage('Install requirements && Unit test') {
            agent { label 'test' }
            steps {
                sh 'cd simple-api/app && pip install -r requirements.txt'
                sh 'cd simple-api && python3 -m unit_test'
            }
        }
        stage('create images of simple-api') {
            agent { label 'test' }
            steps {
                sh 'cd simple-api/app && docker build -t registry.gitlab.com/armza054/test-api .'
            }
        }
        stage('create container of simple-api') {
            agent { label 'test' }
            steps {
                sh 'docker run -d -p 80:5000 registry.gitlab.com/armza054/test-api'
            }
        }
    }
}
