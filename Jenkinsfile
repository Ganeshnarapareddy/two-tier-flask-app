pipeline {
    agent any 

    stages {
        stage('Fetch Code') {
            steps {
                echo 'Pulling code from GitHub...'
                git branch: 'master', url: 'https://github.com/Ganeshnarapareddy/two-tier-flask-app.git'
            }
        }

        stage('Deploy Infrastructure') {
            steps {
                echo 'Running Docker Compose...'
                sh 'docker compose down'
                sh 'docker compose up -d --build'
            }
        }
    }
}
