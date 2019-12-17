pipeline {
    agent {
        docker {
            image 'php'
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
                    php composer.phar install --optimize-autoloader --no-interaction --no-progress --no-ansi --no-suggest
                '''
            }
        }
        stage('test') {
            steps {
                sh 'php vendor/bin/simple-phpunit'
            }
        }
    }
}