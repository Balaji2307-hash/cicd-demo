pipeline {
    agent any
    stages {
        stage('Check Maven Version') {
            steps {
                bat 'mvn -version'
            }
        }
        stage('Clean Build') {
            steps {
                bat 'mvn clean -DskipTests'
            }
        }
        stage('Compile and Package') {
            steps {
                bat 'mvn compile package -DskipTests'
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
                        mvn deploy -DmuleDeploy ^
                        -Dmule.username=Bala_23_07 ^
                        -Dmule.password=Pulsar@2003 ^
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
        }
    }
}