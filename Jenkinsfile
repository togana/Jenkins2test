node('node') {
  def err = null
  currentBuild.result = "SUCCESS"
  try {
    stage 'Checkout'
      checkout scm
    stage 'Test'
      sh 'docker-machine create  -d virtualbox test-jenkins2test'
      sh 'docker-machine regenerate-certs test-jenkins2test'
      sh 'eval $(docker-machine env test-jenkins2test)'
      sh 'docker-compose build'
      sh 'docker-compose run --rm app npm test'
      sh 'docker-machine stop test-jenkins2test'
      sh 'docker-machine rm -f test-jenkins2test'

    stage 'Deploy'
      echo 'ssh to web server and build, up'

    stage 'Cleanup'
      echo 'prune and cleanup'
      sh 'npm prune'
      sh 'rm -rf node_modules'
  }
  catch (caughtError) {
    err = caughtError
    currentBuild.result = "FAILURE"
  }

  finally {
    if (err) {
      throw err
    }
  }
}
