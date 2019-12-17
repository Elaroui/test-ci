pipeline {
    agent { docker { image 'php' } }
    stages {
        stage('build') {
            steps {
                sh '''
                    sudo apt-get install git -yqq zlib1g-dev
                    sudo curl -sS https://getcomposer.org/installer | php
                    sudo php composer.phar install --optimize-autoloader --no-interaction --no-progress --no-ansi --no-suggest
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