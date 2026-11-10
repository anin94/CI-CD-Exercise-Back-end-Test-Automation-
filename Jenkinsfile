
pipeline {
    agent any

    tools {
        nodejs 'NodeJS'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    set -e

                    npm start -- 8888 > app.log 2>&1 &
                    APP_PID=$!

                    trap 'kill $APP_PID 2>/dev/null || true' EXIT

                    sleep 3
                    npm test
                '''
            }
        }
    }
}
