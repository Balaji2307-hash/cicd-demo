pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Application') {
            steps {
                bat 'mvn clean install'
            }
        }
        
        stage('Deploy CloudHubs') {
            environment {
                ANYPOINT_CREDENTIALS = credentials('anypointplatformcredentials')
            }
            steps {
                script {
                    bat """
                        mvn clean deploy -DmuleDeploy ^
                        -Dusername=Bala_23_07 ^
                        -Dpassword=Pulsar@2003^
                        -DworkerType=Micro ^
                        -Dworkers=1
                    """
                }
            }
        }
    }
}