pipeline {
    agent { docker { image 'maven:3.5.4' } }
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World"'

                retry(3) {
                    sh './flakey-deploy.sh'
                }

                timeout(time: 3, unit: 'MINUTES') {
                    sh './health-check.sh'
                }

                sh 'echo "Bye World"'
            }
        }
    }
}
