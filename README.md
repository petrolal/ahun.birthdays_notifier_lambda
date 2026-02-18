# Ahun send month birthdays to telegram.

Lambda function to send monthly Ahun contribuitors birthdays to telegram.

## Usage

### Create S3 bucket to store the lambda code

```bash
aws cloudformation create-stack \
  --stack-name casa-ahun-birthday-bucket-stack \
  --template-body file://casa-ahun-bucket.yaml \
  --parameters ParameterKey=BucketName,ParameterValue=casa-ahun-assets
```

### Create lambda function

```bash
aws cloudformation create-stack \
  --stack-name ahun-birthday-stack \
  --template-body file://template.yaml \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters \
    ParameterKey=S3Bucket,ParameterValue=casa-ahun-assets \
    ParameterKey=S3Key,ParameterValue=ahun-send-monthly-birthdays-to-telegram.zip \
    ParameterKey=SpreadsheetId,ParameterValue='SPREAD_SHEET_ID' \
    ParameterKey=TelegramToken,ParameterValue='TELEGRAM_TOKEN' \
    ParameterKey=ChatId,ParameterValue=2046779343 \
    ParameterKey=GoogleCredentialsJson,ParameterValue='GOOGLE_CREDENTIALS_JSON_ONE_LINE' \
```

### Test the lambda function

```bash
  aws lambda invoke \
    --function-name ahun-send-monthly-birthdays-to-telegram \
    --payload '{}' \
    response.json
```
