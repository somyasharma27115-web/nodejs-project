pipeline {
    agent any

    stages {

        stage('Clone Source Code') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-ssh',
                    url: 'git@github.com:somyasharma27115-web/nodejs-project.git'
            }
        }

        stage('Virtual Environment') {
            steps {
                sh 'python3 -m venv venv'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'venv/bin/pip install -r req.txt'
            }
        }

        stage('Build Flask Application') {
            steps {
                sh 'venv/bin/python -m py_compile app.py'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    pkill -f "venv/bin/python app.py" || true
                    nohup venv/bin/python app.py > flask.log 2>&1 &
                '''
            }
        }
    }
}
