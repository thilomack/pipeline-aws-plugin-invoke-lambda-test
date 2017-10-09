node {
  checkout scm
  try {
    def outputs = cfnUpdate(
      stack:'invoke-lambda-test-stack',
      file:'lambda.yml'
    )
    println outputs;
    println "=== Lambda ==="
    def result = invokeLambda(functionName: outputs.Lambda , payload: [ "Value": "2" ] )
    if (result.Value != 84) {
      error("Wrong value: $result")
    }
    try {
        println "=== FailingLambda ==="
        def result2 = invokeLambda(functionName: outputs.FailingLambda , payload: [ "Value": "2" ] )
        error("no exception: $result2")
    } catch (RuntimeException e) {
        println "Exception:"
        println e
    }
    try {
        println "=== BrokenLambda ==="
        def result2 = invokeLambda(functionName: outputs.BrokenLambda , payload: [ "Value": "2" ] )
        error("no exception: $result2")
    } catch (RuntimeException e) {
        println "Exception:"
        println e
    }
  } finally {
    cfnDelete(stack:'invoke-lambda-test-stack')
  }
}
