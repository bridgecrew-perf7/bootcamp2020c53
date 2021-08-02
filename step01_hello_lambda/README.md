# Deploying Serverless Lambda Functions

## Steps to compile the code

### step 1

make a new folder for your cdk project

```
mkdir step01_hello_lambda

cd step01_hello_lambda
```

### step 2

intialize your cdk project in typescript by running the following command

```
cdk init app --language typescript
```

### step 3

run the following command to build your ts files in real-time. This process needs to keep running in the background so it is best if you run it in a seperate terminal

```
npm run watch
```

### step 4

install aws-lambda

```
npm i @aws-cdk/aws-lambda

npm i @types/aws-lambda

```

add the handler code for your lambda in lambda/hello.ts

```
import { APIGatewayProxyEvent, APIGatewayProxyResult, Context } from 'aws-lambda';

export async function handler(event: APIGatewayProxyEvent, context: Context): Promise<APIGatewayProxyResult> {
  console.log("request:", JSON.stringify(event, undefined, 2));

  return {
    statusCode: 200,
    headers: { "Content-Type": "text/plain" },
    body: `Hello, CDK! You've hit ${event.path}\n`
  };
}
```

### step 5

Initialize your lambda function

```
  const hello = new lambda.Function(this, "HelloHandler", {
      runtime: lambda.Runtime.NODEJS_10_X,
      code: lambda.Code.fromAsset("lambda"),
      handler: "hello.handler",
    });

```

---

This is a blank project for TypeScript development with CDK.

The `cdk.json` file tells the CDK Toolkit how to execute your app.

## Useful commands

- `npm run build` compile typescript to js
- `npm run watch` watch for changes and compile
- `npm run test` perform the jest unit tests
- `cdk deploy` deploy this stack to your default AWS account/region
- `cdk diff` compare deployed stack with current state
- `cdk synth` emits the synthesized CloudFormation template
