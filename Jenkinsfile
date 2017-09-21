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
  } finally {
    cfnDelete(stack:'invoke-lambda-test-stack')
  }
}
