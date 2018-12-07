pipeline {
    agent { docker { image 'maven:3.5.4' } }
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'

                timeout(time: 3, unit: 'MINUTES') {
                    retry(3) {
                        sh 'echo "Hello..."'
                    }
                }
                
                sh 'echo "Bye World"; exit 0'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
            }
        }
        stage('Deploy - Staging') {
            steps {
                echo 'Deploying to staging'
            }
        }
        stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
        }
        stage('Deploy - Production') {
            steps {
                echo 'Deploying to production'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
            mail to: 'james.wang@optum.com',
                subject: "Successful Pipeline: ${currentBuild.fullDisplayName}",
                body: "BUILD_URL: ${env.BUILD_URL}"
        }
        failure {
            echo 'This will run only if failed'
            mail to: 'james.wang@optum.com',
                subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                body: "Something is wrong with ${env.BUILD_URL}"
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            sh 'echo -e "This will run only if the state of the Pipeline has changed.\nFor example, if the Pipeline was previously failing but is now successful."'
        }
    }
}
