pipeline {
    agent { docker { image 'php' } }
    stages {
        stage('build') {
            steps {
                sh '''
                    mount -o remount,exec /var
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