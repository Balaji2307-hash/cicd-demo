pipeline {
    agent any
    stages {
        stage('Check Versions') {
            steps {
                bat 'mvn -version'
                bat 'java -version'
            }
        }
        stage('Build Application') {
            steps {
                bat 'mvn clean compile -DskipTests'
            }
        }
        stage('Package Application') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }
        stage('Deploy to CloudHub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'anypointplatformcredentials', 
                        usernameVariable: 'Bala_23_07', 
                        passwordVariable: 'Pulsar@2003'
                    )
                ]) {
                    bat """
                        mvn deploy -DmuleDeploy ^
                        -Dmule.username=%MULE_USERNAME% ^
                        -Dmule.password=%MULE_PASSWORD% ^
                        -DskipTests
                    """
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed'
        }
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed. Check logs for details.'
            bat 'mvn -version'
        }
    }
}