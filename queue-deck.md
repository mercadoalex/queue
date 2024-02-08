#Deploy a queue via CDK app stack

````
mkdir queue
cd queue
cdk init app --language=typescript
cdk deploy
aws sqs list-queues
q=$(aws sqs list-queues --query "QueueUrls[0]" --output text)
echo $q
aws sqs receive-message --queue-url $q --wait-time-seconds 20
aws sqs send-message --queue-url $q --message-body "hola, mundo cruel"
cdk destroy --force

```