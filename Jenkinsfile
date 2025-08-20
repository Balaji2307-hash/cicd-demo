pipeline {
  agent any

  options {
    ansiColor('xterm')
    timestamps()
  }

  tools {
   
  }

  environment {
  }

  stages {
    stage('Checkout') {
     
    }

    stage('Build Application') {
      steps {
        bat 'mvn -V -B clean install'
      }
    }

    stage('Deploy CloudHub') {
      environment {
        
        ANYPOINT_CREDENTIALS = credentials('anypointplatformcredentials')
      }
      steps {
        echo 'Deploying mule project due to the latest code commit…'
        echo 'Deploying to the configured environment….'

          mvn -B clean deploy ^
            -DmuleDeploy ^
            -Dusername=%Bala_23_07% ^
            -Dpassword=%Pulsar@2003% ^
            -Denvironment=Sandbox ^
            -DconnectedApp=false ^
            -Dapplication.name=cicd-demo ^
            -DworkerType=Micro ^
            -Dworkers=1
        """
      }
    }
  }

  post {
    success {
      echo 'Build and deployment completed successfully.'
    }
    failure {
      echo 'Build or deployment failed. Check logs for details.'
    }
    always {
      archiveArtifacts artifacts: '**/target/*.jar, **/target/*.zip, **/target/*.tar.gz', allowEmptyArchive: true
      junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
    }
  }
}
