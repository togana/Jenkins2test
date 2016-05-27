node {
  def err = null
  currentBuild.result = "SUCCESS"
  try {
    stage 'Checkout'
      checkout scm
    stage 'Test'
      sh 'docker-machine create -d virtualbox test-jenkins2test'
      sh 'docker-machine regenerate-certs -f test-jenkins2test'
      sh '
        eval $(docker-machine env test-jenkins2test) && \
        docker-compose build && \
        docker-compose run --rm app npm test'

    stage 'Deploy'
      echo 'ssh to web server and build, up'

  }
  catch (caughtError) {
    err = caughtError
    currentBuild.result = "FAILURE"
  }

  finally {
    sh 'docker-machine stop test-jenkins2test'
    sh 'docker-machine rm -f test-jenkins2test'
    if (err) {
      throw err
    }
  }
}
