## how to start

```bash
# for the first time
$ npm install -g dynamodb-admin

# start dynamodb
$ docker-compose up -d

# let's visit console
## for inserting data and checking docs
$ open http://localhost:8000/shell/ 
## for checking data in database
$ DYNAMO_ENDPOINT=http://localhost:8000 dynamodb-admin


# insert test data
$ open http://localhost:8000/shell/
# copy and paste javascript code below and run
```

```javascript
var allRequestItems = [
    // copy and paste lines from dynamodb/reaction.json here
];

function batchWrite(requestItems) {
    var params = {
        RequestItems: {
            reactions: requestItems
        },
        ReturnConsumedCapacity: 'NONE',
        ReturnItemCollectionMetrics: 'NONE',
    };
    docClient.batchWrite(params, function(err, data) {
        if (err) ppJson(err); // an error occurred
        else ppJson(data); // successful response
    });
} 

while(allRequestItems.length > 0) {
    console.log(allRequestItems.length)
    batchWrite(allRequestItems.splice(0, 15));
}
```