pipeline {
    agent any
    stages {
        stage('Clean Maven Cache') {
            steps {
                bat 'mvn dependency:purge-local-repository -DactTransitively=false -DreResolve=false -DfailOnError=false'
            }
        }
        stage('Verify Plugin Availability') {
            steps {
                bat 'mvn org.mule.tools.maven:mule-maven-plugin:3.9.4:help -U'
            }
        }
        stage('Compile and Package') {
            steps {
                bat 'mvn clean compile package -DskipTests -U'
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
                        -Dmule.username=Bala_23_07 ^
                        -Dmule.password= Pulsar@2003^
                        -DskipTests -U
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
            bat 'mvn org.mule.tools.maven:mule-maven-plugin:3.9.4:help -U'
        }
    }
}