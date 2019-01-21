# ReddCoin Node API
ReddCoin API LIB that exposes `reddcoind` JSON-RPC Methods through a simply structured URL driven API.

## Install
You can include the `reddcoin-node-api` easily in your node.js project.
```javascript
npm install reddcoin-node-api
```

## Example Use
You can use `reddcoin-node-api' to expose the reddcoind JSON-RPC through a easy to work with URL Structure/
### Node (API Instances)

```javascript
var rddapi = require('reddcoin-node-api'),
express = require('express'),
app = express();

// Username and Password can be set in `~/.reddcoin/reddcoin.conf`
var rddacc = {
  host: 'localhost',
  port: 45443,
  user: 'reddcoinrpc',
  pass: 'rddcoinpass'
};

var path = '/api';

rddapi.setWalletDetails(rddacc);
rddapi.setAccess('default-safe');
app.use(path, rddapi.app); 

app.listen(5000);
```

### Using the API Instance
You can call methods from the `reddcoind` JSON-RPC API using a simple URL Structure.
```
  http://localhost:5000/PATH/METHOD
  
```

### Calling the API Without Parameters
```
  http://localhost:5000/api/getinfo
```
Would result in a response exactly the same as if were called by the JSON-RPC its self.
```
{
  "version": 1,
  "protocolversion": 1,
  "walletversion": 1,
  "balance": 1,
  "blocks": 112345,
  "timeoffset": -2,
  "connections": 8,
  "proxy": "",
  "testnet": false,
  "keypoololdest": 1368414896,
  "keypoolsize": 101,
  "paytxfee": 0.0001,
  "unlocked_until": 0,
  "errors": ""
}
```

#### Calling the API With Parameters
Sometimes you may need to send parameters with your request this can be done in the query string like in the following example call to `getTransaction` The parameters match up with those of the `reddcoind` JSON-RPC documentation.

```
http://localhost:5000/api/gettransaction?txid=TXID
```

### Access Control
The `only` type restricts method calls to only those in the methods object.
```
  rddapi.setAccess('only', ['getinfo']);
```

Restricting access to certian methods can be done using the `restrict` type.
```
  rddapi.setAccess('restrict', ['dumpprivkey', 'sendmany']);
```

Restrict `reddcoin-node-api` to only call `read-only` methods.
```
  rddapi.setAccess('read-only');
```