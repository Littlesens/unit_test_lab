pipeline {
    agent {
        docker {
            image 'composer:latest'
        }
    }
    stages {
        stage('Build') {
            steps {
                script {
                    // Navigate to the directory containing composer.json
                    dir('jenkins-phpunit-test') {
                        sh 'composer install'
                    }
                }
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
            junit testResults: 'logs/unitreport.xml'
        }
    }
}
