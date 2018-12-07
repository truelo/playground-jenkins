pipeline {
    agent { docker { image 'maven:3.5.4' } }
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World"'

                timeout(time: 3, unit: 'MINUTES') {
                    retry(5) {
                        sh './flakey-deploy.sh'
                    }
                }
                
                sh 'echo "Bye World"'
            }
        }
    }
}
