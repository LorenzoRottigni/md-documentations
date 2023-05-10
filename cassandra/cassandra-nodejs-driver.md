# NodeJS - cassandra-driver

### Install node_module of cassandra driver:
` npm install cassandra-driver `

### Import node_module:
` const cassandra = require('cassandra-driver'); `

### Define cassandra authentication variable:
` var authProvider = new cassandra.auth.PlainTextAuthProvider('cassandra', 'cassandra'); `

By default cassandra username and password are cassandra cassandra.

### Define contactsPoints with the server where cassandra is deployed:
`var contactPoints = ['10.70.70.120:9042'];`

My cassandraDB is deployed on my personal server 10.70.70.120.
Cassandra runs in a Docker container binded to external port 9042

### Define client connection parameters:

```
var client = new cassandra.Client({
  //var contactPoints
  contactPoints: contactPoints,
  //my cassandra datacenter is named datacenter1
  localDataCenter: 'datacenter1',
  //var authProvider
  authProvider: authProvider,
  //name of the keyspace
  keyspace:'lorenzo_keyspace'
});

```

### Test DB connection:

```
client.connect().then(()=>{
  //connected property is true if connections is established
  console.dir(client.connected)
}).catch((err)=>{
  //print connection errors
  console.dir(err)
  //if connection not established is false
  console.dir(client.connected)
})
```
