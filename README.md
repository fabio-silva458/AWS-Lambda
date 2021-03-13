# AWS Lambda em Typescript com Serverless Framework

Função Lambda simples em Typescript usando o Serverless Framework para implantar.

https://docs.aws.amazon.com/lambda/latest/dg/lambda-nodejs.html

## Desenvolvimento

```
$ serverless create --template aws-nodejs --path serverless-typescript
$ npm install -D serverless-plugin-typescript typescript
$ npm install -D serverless-offline

$ serverless invoke local --function serverlessTypescript --log
$ serverless offline start
```

## Implantar

```
$ serverless deploy
```

O resultado esperado deve ser semelhante a:

```
Serverless: Compiling with Typescript...
Serverless: Using local tsconfig.json
handler.ts (1,25): Cannot find module 'aws-lambda' or its corresponding type declarations.
Serverless: Typescript compiled.
Serverless: Packaging service...
Serverless: Excluding development dependencies...
Serverless: Creating Stack...
Serverless: Checking Stack create progress...
........
Serverless: Stack create finished...
Serverless: Uploading CloudFormation file to S3...
Serverless: Uploading artifacts...
Serverless: Uploading service serverless-typescript.zip file to S3 (13.92 MB)...
Serverless: Validating template...
Serverless: Updating Stack...
Serverless: Checking Stack update progress...
..............................
Serverless: Stack update finished...
Service Information
service: serverless-typescript
stage: dev
region: eu-central-1
stack: serverless-typescript-dev
resources: 11
api keys:
  None
endpoints:
  GET - https://m92rf2g2j4.execute-api.eu-central-1.amazonaws.com/dev/
functions:
  serverlessTypescript: serverless-typescript-dev-serverlessTypescript
layers:
  None
```

## Uso

Agora você pode invocar a função Lambda diretamente e até mesmo ver o log resultante via

```
serverless invoke --function serverlessTypescript --log
```

O resultado esperado deve ser semelhante a:

```
{
    "statusCode": 200,
    "body": "{\n  \"message\": \"Hello Serverless Typescript.\",\n  \"input\": {}\n}"
}
--------------------------------------------------------------------
START RequestId: 1aa539db-6ec8-4be7-9f6d-3492811b82e7 Version: $LATEST
END RequestId: 1aa539db-6ec8-4be7-9f6d-3492811b82e7
REPORT RequestId: 1aa539db-6ec8-4be7-9f6d-3492811b82e7	Duration: 2.40 ms	Billed Duration: 100 ms	Memory Size: 512 MB	Max Memory Used: 65 MB	Init Duration: 152.52 ms
```

Finalmente, você pode enviar uma solicitação HTTP diretamente para o endpoint usando uma ferramenta como curl ou HTTPie

```
$ http get https://XXXXXXXXXX.execute-api.eu-central-1.amazonaws.com/dev/serverless-typescript
```