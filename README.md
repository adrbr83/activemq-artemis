# activemq-artemis
ActiveMq Artemis Rest Api Examples


# Create Queue
```
curl -u "user:password" -X POST "https://<host>:<port>/console/jolokia/exec" \
-H "Content-Type: application/json" \
-d '{
    "type": "EXEC",
    "mbean": "org.apache.activemq.artemis:broker=\"broker-name\"",
    "operation": "createQueue(java.lang.String,java.lang.String,java.lang.String)",
    "arguments": [
        "queue_test_name",      // Address
        "queue_test_name",      // Name
        "ANYCAST"               // Routing Type
    ]
}'
```


# Deploy Queue
```
curl -u "user:password" -X POST "https://<host>:<port>/console/jolokia/exec" \
-H "Content-Type: application/json" \
-d '{
    "type": "EXEC",
    "mbean": "org.apache.activemq.artemis:broker=\"broker-name\"",
    "operation": "deployQueue(java.lang.String,java.lang.String,java.lang.String,boolean)",
    "arguments": [
        "queue_test_name",      
        "queue_test_name",      
        "",                
        true               
    ]
}'
```

# Move Messages
```
curl -u "user:password" -X POST "https://<host>:<port>/console/jolokia/exec" -H "Content-Type: application/json" -d '{
    "type": "EXEC",
    "mbean": "org.apache.activemq.artemis:broker=\"broker-name\",component=addresses,address=\"source_queue\",subcomponent=queues,routing-type=\"anycast\",queue=\"source_queue\"",
    "operation": "moveMessages(java.lang.String,java.lang.String)",
    "arguments": ["", "destination_queue"]
}'
```



# List Queues
```
curl -s -u "user:password" "https://<host>:<port>/console/jolokia/read/org.apache.activemq.artemis:broker=%22<broker-name>%22/QueueNames"

```

# Count Messages
```
curl -u "user:password" -X POST "https://<host>:<port>/console/jolokia/exec" -H "Content-Type: application/json" -d '{
    "type": "EXEC",
    "mbean": "org.apache.activemq.artemis:broker=\"<broker-name>\",component=addresses,address=\"<adress_name>\",subcomponent=queues,routing-type=\"anycast\",queue=\"<queue_name>\"",
    "operation": "countMessages(java.lang.String)",
    "arguments": [
        "" // filter
    ]
}' 
```

# Remove / Delete Messages
```
curl -u "user:password" -X POST "https://<host>:<port>/console/jolokia/exec" -H "Content-Type: application/json" -d '{
    "type": "EXEC",
    "mbean": "org.apache.activemq.artemis:broker=\<broker-name>\",component=addresses,address=\"<adress_name>\",subcomponent=queues,routing-type=\"anycast\",queue=\"<queue_name>\"",
    "operation": "removeMessages(java.lang.String)",
    "arguments": ["AMQTimestamp<1730731343001"]
}'
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

# Send a message
```
curl -X POST \
  -u "user:password" \
  "https://<host>:<port>/console/jolokia/exec" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "EXEC",
    "mbean": "org.apache.activemq.artemis:broker=\"<broker-name>\",component=addresses,address=\"<adress_name>\",subcomponent=queues,routing-type=\"anycast\",queue=\"<queue_name>\"",
    "operation": "sendMessage(java.util.Map,int,java.lang.String,boolean,java.lang.String,java.lang.String)",
    "arguments": [
      {"header" : "test"},                  
      0,                   
      "VGVzdCBNZXNzYWdlIEJvZHkK", // base64
      true,               
      "user",            
      "pass"       
    ]
  }'
```
