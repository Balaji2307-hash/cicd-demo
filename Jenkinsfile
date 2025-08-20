pipeline {
    agent any
    environment {
        MULE_USERNAME = credentials('Bala_23_07')
        MULE_PASSWORD = credentials('Pulsar@2003')
    }
    stages {
        stage('Deploy') {
            steps {
                script {
                    sh '''
                        mvn clean package deploy -DmuleDeploy \
                        -Dmule.username=${MULE_USERNAME} \
                        -Dmule.password=${MULE_PASSWORD} \
                        -Dmule.environment=dev
                    '''
                }
            }
        }
    }
}