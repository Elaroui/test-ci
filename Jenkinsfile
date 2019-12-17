pipeline {
    agent { docker { image 'php' } }
    stages {
        stage('build') {
            steps {
                sh '''
                    chmod -R 755 var/www/html
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