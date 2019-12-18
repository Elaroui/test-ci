pipeline {
    agent {
        docker {
            image 'php:7.2-cli'
            args '-u root:sudo'
        }
    }
    stages {
        stage('build') {
            steps {
                sh '''
                    apt-get update -yqq
                    apt-get install git -yqq zlib1g-dev
                    curl -sS https://getcomposer.org/installer | php
                '''
                timeout(time: 20, unit: 'MINUTES') {
                    sh 'php composer.phar install --optimize-autoloader --no-interaction --no-progress --no-ansi --no-suggest'
                }
            }
        }
        stage('test') {
            steps {
                sh 'php vendor/bin/simple-phpunit'
            }
        }
        stage('review') {
            steps {
                sh 'php vendor/bin/phpcs --report=summary --standard=PSR12 ./src/AppBundle'
            }
        }
    }
}