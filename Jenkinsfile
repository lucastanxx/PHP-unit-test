pipeline {
    agent none // Use 'none' if specifying agent later at each stage or globally here if every stage will use the same
    stages {
        stage('Build') {
            agent {
                docker { image 'composer:latest' }
            }
            steps {
                sh 'composer install'
            }
        }
        stage('Test') {
            agent {
                docker { image 'composer:latest' }
            }
            steps {
                sh './vendor/bin/phpunit tests'
            }
        }
    }
}
