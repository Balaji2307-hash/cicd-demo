pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('Deploy CloudHub') {
            steps {
                echo 'Deploying mule project due to the latest code commit…'
                echo 'Deploying to the configured environment….'
                withCredentials([usernamePassword(
                    credentialsId: 'anypointplatformcredentials',
                    usernameVariable: 'Bala_23_07',
                    passwordVariable: 'Pulsar@2003'
                )]) {
                    bat "mvn clean deploy -DmuleDeploy -Dusername=%ANYPOINT_USERNAME% -Dpassword=%ANYPOINT_PASSWORD% -DworkerType=Micro -Dworkers=1"
                }
            }
        }
    }
}