# Serverless Offline

## Prerequisites
1. Install npm
2. Install Serverless Framework CLI

## Steps
1. Run `mkdir serverless-offline`
2. Run `cd serverless-offline`
3. Run `npm init` and choose default values
4. Run `npm install --save-dev serverless-offline`
5. Create `serverless.yml` file in root folder and add following content:
```
service: hello-world-offline

provider:
  name: aws
  runtime: nodejs12.x
  region: us-west-2
  memorySize: 1024
  stage: dev

plugins:
  - serverless-offline

functions:
  hello-world:
    handler: libs/index.helloWorld
    name: "${self:service}-${self:provider.stage}"
    description: "Hello World Example"
    events:
      - http:
          path: hello-world
          method: get
          cors: true

```
6. Create `libs/index.js` and add following content:
```
module.exports.helloWorld = async (event) => {
    return {
        statusCode: 200,
        body: "Hello World!",
    };
};
```
7. Run `sls offline start`
8. Go to browser and open URL `http://localhost:3000/dev/hello-world`
