pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/lucastanxx/PHP-unit-test.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'docker run --rm -v $(pwd):/app -w /app composer install'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm -v $(pwd):/app -w /app php:7.4-cli ./vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
            }
        }
    }

    post {
        always {
            script {
                junit 'logs/unitreport.xml'
                archiveArtifacts artifacts: 'logs/unitreport.xml', fingerprint: true
            }
        }
    }
}
