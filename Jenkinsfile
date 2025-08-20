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
            steps {
                bat """
                    mvn clean deploy -DmuleDeploy ^
                    -Dusername=Bala_23_07 ^
                    -Dpassword=Pulsar@2003 ^
                    -DdeploymentTarget=cloudhub-2.0 ^
                    -Dapplication.name=cicd-demo ^
                    -DworkerType=Micro ^
                    -Dworkers=1 ^
                    -Druntime=4.7.2
                """
            }
        }
    }
}