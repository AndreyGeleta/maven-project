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

        stage('Deploy') {
            steps {
                echo 'Code deploy.'
            }
        }
    }

}
