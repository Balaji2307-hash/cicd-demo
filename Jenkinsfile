stage('Deploy CloudHub') {
  steps {
    echo "Deploying Mule project to ${env.MULE_ENV}…"
    bat '''
      mvn clean deploy -DmuleDeploy ^
        -Dusername=%Bala_23_07% ^
        -Dpassword=%Pulsar@2003% ^
        -Denvironment=%SandBox% ^
        -DworkerType=%Micro% ^
        -Dworkers=%1%
    '''
  }
}
