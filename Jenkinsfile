node {
  def err = null
  currentBuild.result = "SUCCESS"
  try {
    stage 'Checkout'
      echo 'checkout'
    stage 'Test'
      echo 'TEST'
    stage 'Deploy'
      echo 'ssh to web server and build, up'

    stage 'Cleanup'
      echo 'prune and cleanup'
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
