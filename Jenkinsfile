pipeline {
    agent { docker { image 'maven:3.5.4' } }
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World"'

                timeout(time: 3, unit: 'MINUTES') {
                    retry(3) {
                        sh 'echo "Hello..."'
                    }
                }
                
                sh 'echo "Bye World"'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
