pipeline {
    agent any
    tools {
        maven 'M3'  // Make sure Maven 3.6.3+ is configured in Jenkins
    }
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
                        usernameVariable: 'MULE_USERNAME', 
                        passwordVariable: 'MULE_PASSWORD'
                    )
                ]) {
                    bat """
                        mvn deploy -DmuleDeploy \
                        -Dmule.username=Bala_23_07 \
                        -Dmule.password=Pulsar@2003 \
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