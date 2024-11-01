# activemq-artemis
ActiveMq Artemis Rest Api Examples

# Create Queue
```
curl -u "user:password" -X POST "https://<host>:<port>/console/jolokia/exec" \
-H "Content-Type: application/json" \
-d '{
    "type": "EXEC",
    "mbean": "org.apache.activemq.artemis:broker=\"primary-2\"",
    "operation": "deployQueue(java.lang.String,java.lang.String,java.lang.String,boolean)",
    "arguments": [
        "queue_test_name",      
        "queue_test_name",      
        "",                
        true               
    ]
}'
```

# List Queues
```
curl -s -H "Origin:http://localhost" -u "user:password" "https://<host>:<port>/console/jolokia/read/org.apache.activemq.artemis:broker=%22<broker-name>%22/QueueNames" | jq .

```

# Delete Queue
```
curl -u "user:password" -X POST "https://<host>:<port>/console/jolokia/exec" -H "Content-Type: application/json" -d '{
    "type": "EXEC",
    "mbean": "org.apache.activemq.artemis:broker=\"<broker-name>\"",
    "operation": "destroyQueue(java.lang.String,boolean,boolean)",
    "arguments": [
        "queue_test_name",
        true,
        true
    ]
}'
```
