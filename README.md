# Example Step Function - Synchronous Integration with API Gateway

API Gateway provides integration with Step Functions, Standard or Express. In this example I'll cover synchronous integration using type Step Function type EXPRESS (since this is the only one who supports sync calls).
<hr>
<p align="center">
The steps executed is quite simple
</p>

<img src="https://github.com/stefanycos/aws-step-functions-demo/blob/main/resources/stepfunction-apigateway.drawio.png" alt="drawing" width="800"/>

### Important points to consider in this integration

- API Gateway: 
  - When calling the step function to pass the received information, like queryparametes or headers, for exemple, we need to map a template with a json containing a property **input**, the **input** property is the attribute received by step function.
  - Redirect to step function is done using the property stateMachineArn, in this example I configured in the template, but see that this isn't the only way to configure it.
  ```json
    {
      "stateMachineArn": "arn:aws:states:us-east-1:564604832395:stateMachine:ValidateUserStepFunctionExpress",
      "input": "{\"version\": $input.params('version'), \"params\": \"$input.params()\"}"
    }
    
- Step Function:
  - Unlike Standard Step Functions, express type doesn't offer the possibility of seing the executions (including it's input and output) direct in the console, so the analysis has to be done using only logs.
  
### Creating Stack

File **template.yaml** contains the creation of all resources:

- API Gateway
- Step Function
- All Required Roles
- Lambdas (with a simple code that can be available for edition in lambda console)

Once the stack is created the URL to call the API Gateway will be provided at Cloudformation Outouts tab
**Important:** after performing your tests don't forget to clean up your environment deleting the stack created.
