pipeline {
    agent any
    stages{
        stage('init') {
            steps {
                echo "Testing ..."
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving ...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Code deploy.'
                build job: 'deploy_to_staging'
            }
        }

        stage('Deploy to Production') {
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }

                build job: 'deploy_to_prod'
            }
            post {
                sucess {
                    echo 'Code deployed to Production'
                }

                failure {
                    echo 'Deployment failed'
                }
            }
        }
    }

}
