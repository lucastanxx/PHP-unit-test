pipeline {
    agent {
        docker {
            image 'composer:latest'
        }
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/lucastanxx/PHP-unit-test.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'composer install'
            }
        }

        stage('Test') {
            steps {
                sh './vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
            }
        }
    }

    post {
        always {
            junit 'logs/unitreport.xml'  // Specify the path to the JUnit report
            archiveArtifacts artifacts: 'logs/unitreport.xml', fingerprint: true
        }
    }
}
