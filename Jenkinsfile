pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/reshreshu/setup_ci.git'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running test script...'
                sh 'chmod +x test.sh'
                sh './test.sh'
            }
        }

        stage('Build HTML Page') {
            steps {
                echo 'Copying HTML and CSS to output folder...'
                sh 'mkdir -p output && cp index.html style.css output/'
            }
        }

        stage('Archive HTML') {
            steps {
                echo 'Archiving HTML output...'
                archiveArtifacts artifacts: 'output/**', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline finished successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check the logs for errors.'
        }
    }
}
