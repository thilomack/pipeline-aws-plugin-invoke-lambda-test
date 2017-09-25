node {
  checkout scm
  try {
    def outputs = cfnUpdate(
      stack:'invoke-lambda-test-stack',
      file:'lambda.yml'
    )
    println outputs;
    def result = invokeLambda(functionName: outputs.Lambda , payload: [ "Value": "2" ] )
    if (result.Value != 84) {
      error("Wrong value: $result")
    }
    try {
        def result2 = invokeLambda(functionName: outputs.FailingLambda , payload: [ "Value": "2" ] )
        println result2
    } catch (RuntimeException e) {
        println e
    }
    try {
        def result2 = invokeLambda(functionName: outputs.BrokenLambda , payload: [ "Value": "2" ] )
        println result2
    } catch (RuntimeException e) {
        println e
    }
  } finally {
    cfnDelete(stack:'invoke-lambda-test-stack')
  }
}
