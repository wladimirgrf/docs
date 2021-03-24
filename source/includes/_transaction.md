# Transaction API

Transactions are grouped into blocks and about every 10 minutes, a new block of transactions is sent out, becoming part of the transaction log (Blockchain), which indicates the transaction has been made (more-or-less) official. Once a transaction has been successfully mined in the blockchain, you can say that you transferred a certain amount of BTC to another address.

BitChain's Transaction API allows you to look up information about unconfirmed transactions, query transactions based on their id (hash), create and propagate your own transactions. 

## Transaction Endpoint

The Transaction Endpoint returns detailed information about a given transaction based on its public id (hash).

### HTTP Request

<div class="endpoint">
  <i>GET</i>
  <span>https://testnet.bitchain.network/transactions/:id</span>
</div>


```shell
curl "https://testnet.bitchain.network/transactions/d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53"
```

```javascript
const axios = require('axios');

const api = axios.create({
  baseURL: "https://testnet.bitchain.network",
});

api.get('/transactions/d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53').then(function (response) {
  console.log(response.data);
});
```

```java
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;

...

var baseURL = "https://testnet.bitchain.network";

var uri = String.format("%s/transactions/d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53",baseURL);

HttpClient client = HttpClient.newHttpClient();
HttpRequest request=HttpRequest.newBuilder()
  .header("content-type","application/json")
  .uri(URI.create(uri))
  .GET()
  .build();

HttpResponse<String> response = client.send(request,HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
```

```php
<?php

$url = "https://testnet.bitchain.network/transactions/d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53";

$curl = curl_init($url);
curl_setopt($curl, CURLOPT_URL, $url);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);

$resp = curl_exec($curl);
curl_close($curl);
var_dump($resp);

?>
```


### URL Parameters

Parameter | Description
--------- | -----------
`id`    | The id is a string representing the hex-encoded transaction hash you're interested in querying

` Example: d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53`

```json
{
  "id": "d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53",
  "fee": 24547,
  "confirmations": 1194,
  "date": "2021-03-02T21:02:23.000Z",
  "transactionInput": [
    {
      "address": "tb1q3yyq37lalgq0chareur9yykgtgpqwztt5uezvz",
      "value": 78836818
    },
    {
      "address": "tb1qrgrmt8cm6n7nhqz9lexvy0rxul0xr52m2gay0u",
      "value": 71923196
    }
  ],
  "transactionOutput": [
    {
      "address": "mhfNudm6YDYnYkegFSjcsppucpAA8TRviD",
      "value": 100000000
    },
    {
      "address": "tb1q7zf06fvr8jq889k3v6ly2l0slxphtuka6dlmcs",
      "value": 50735467
    }
  ]
}
```

### HTTP Response

A Transaction represents the current state of a particular transaction from either a Block within a Blockchain, or an unconfirmed transaction that has yet to be included in a Block.

Attribute          | Type      | Description
---------          | ----      | -----------
`id`               | string  | Is a string representing the hex-encoded transaction hash.
`fee`              | integer | The total number of fees in satoshis, collected by miners in this transaction.
`confirmations`    | integer | Number of subsequent blocks, including the block the transaction is in. Unconfirmed transactions have 0 confirmations.
`date`             | string  | Time this transaction was received by the Blockchain provider.
`transactionInput` | array[[TransactionInput](#transactioninput)]   | Array of Wallets that spend some amount in this transaction.
`transactionOutput`| array[[TransactionOutput](#transactionoutput)] | Array of Wallets that received some amount in this transaction.

#### On the right side, you will find an example of the object returned in the response you will get from the server.


## Transaction Fee Endpoint

The Transaction Fee Endpoint returns the estimated mining fee amount (in satoshis) for a transaction, based on the addresses and value involved.

### HTTP Request

<div class="endpoint">
  <i>POST</i>
  <span>https://testnet.bitchain.network/transactions/fee</span>
</div>


```shell
curl -X POST -H "Content-Type: application/json" -d '{"addressFrom": "muwAf337HUDpuajeA2yERod4bPZyWpcqbd","addressTo": "mjDaJzEDCjiS86jJWmpn38nGe2A9N7EStd","value": 10000}' "https://testnet.bitchain.network/transactions/fee"
```

```javascript
const axios = require('axios');

const api = axios.create({
  baseURL: "https://testnet.bitchain.network",
});

api.post('/transactions/fee', {
  addressFrom: "muwAf337HUDpuajeA2yERod4bPZyWpcqbd",
  addressTo: "mjDaJzEDCjiS86jJWmpn38nGe2A9N7EStd",
  value: 10000
}).then(function (response) {
  console.log(response.data);
});
```

```java
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;

...

var baseURL = "https://testnet.bitchain.network";

var uri = String.format("%s/transactions/fee",baseURL);
var json = "{"
  +"\"addressFrom\": \"muwAf337HUDpuajeA2yERod4bPZyWpcqbd\","
  +"\"addressTo\": \"mjDaJzEDCjiS86jJWmpn38nGe2A9N7EStd\","
  +"\"value\": 10000"
+"}";

HttpClient client = HttpClient.newHttpClient();
HttpRequest request=HttpRequest.newBuilder()
  .header("content-type","application/json")
  .uri(URI.create(uri))
  .POST(HttpRequest.BodyPublishers.ofString(json))
  .build();

HttpResponse<String> response = client.send(request,HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
```

```php
<?php

$url = "https://testnet.bitchain.network/transactions/fee";

$curl = curl_init($url);
curl_setopt($curl, CURLOPT_URL, $url);
curl_setopt($curl, CURLOPT_POST, true);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);

$headers = array(
   "Content-Type: application/json",
);
curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);

$data = <<<DATA
{
  "addressFrom":"muwAf337HUDpuajeA2yERod4bPZyWpcqbd",
  "addressTo": "mjDaJzEDCjiS86jJWmpn38nGe2A9N7EStd",
  "value": 10000
}
DATA;

curl_setopt($curl, CURLOPT_POSTFIELDS, $data);

$resp = curl_exec($curl);
curl_close($curl);
var_dump($resp);

?>
```


### Body

Attribute     | Type    | Description
---------     | ----    | -----------
`addressFrom` | string  | It is a string that represents the public address of a wallet that has a value to spend.
`addressTo`   | string  | It is a string that represents the public address of the wallet that you want to send the amount.
`value`       | integer | The value received in this transaction, in satoshis.

```json
{
  "transactionEstimatedFee": 31300
}
```

### HTTP Response

Attribute                 | Type      | Description
---------                 | ----      | -----------
`transactionEstimatedFee` | integer | The estimated mining fee amount for the transaction, in satoshis.

#### On the right side, you will find an example of the object returned in the response you will get from the server.


## Create Transaction Endpoint

Using BitChain's API, you can push transactions to blockchain. 

<aside class="success">
We never take possession of your private keys.
</aside>

### HTTP Request

<div class="endpoint">
  <i>POST</i>
  <span>https://testnet.bitchain.network/transactions/create</span>
</div>


```shell
curl -X POST -H "Content-Type: application/json" -d '{"privateKey": "cW33mrcvCY2YzoFegug4xfQ8U4yNEAeLRUs2z78ZwCwb4w1Fn35K","addressTo": "muwAf337HUDpuajeA2yERod4bPZyWpcqbd","value": 1000}' "https://testnet.bitchain.network/transactions/create"
```

```javascript
const axios = require('axios');

const api = axios.create({
  baseURL: "https://testnet.bitchain.network",
});

api.post('/transactions/create', {
  privateKey: "cW33mrcvCY2YzoFegug4xfQ8U4yNEAeLRUs2z78ZwCwb4w1Fn35K",
  addressTo: "muwAf337HUDpuajeA2yERod4bPZyWpcqbd",
  value: 1000
}).then(function (response) {
  console.log(response.data);
});
```

```java
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;

...

var baseURL = "https://testnet.bitchain.network";

var uri = String.format("%s/transactions/create",baseURL);
var json = "{"
  +"\"privateKey\": \"cW33mrcvCY2YzoFegug4xfQ8U4yNEAeLRUs2z78ZwCwb4w1Fn35K\","
  +"\"addressTo\": \"muwAf337HUDpuajeA2yERod4bPZyWpcqbd\","
  +"\"value\": 1000"
+"}";

HttpClient client = HttpClient.newHttpClient();
HttpRequest request=HttpRequest.newBuilder()
  .header("content-type","application/json")
  .uri(URI.create(uri))
  .POST(HttpRequest.BodyPublishers.ofString(json))
  .build();

HttpResponse<String> response = client.send(request,HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
```

```php
<?php

$url = "https://testnet.bitchain.network/transactions/create";

$curl = curl_init($url);
curl_setopt($curl, CURLOPT_URL, $url);
curl_setopt($curl, CURLOPT_POST, true);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);

$headers = array(
   "Content-Type: application/json",
);
curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);

$data = <<<DATA
{
  "privateKey":"cW33mrcvCY2YzoFegug4xfQ8U4yNEAeLRUs2z78ZwCwb4w1Fn35K",
  "addressTo": "mjDaJzEDCjiS86jJWmpn38nGe2A9N7EStd",
  "value": 1000
}
DATA;

curl_setopt($curl, CURLOPT_POSTFIELDS, $data);

$resp = curl_exec($curl);
curl_close($curl);
var_dump($resp);

?>
```


### Body

Attribute    | Type    | Description
---------    | ----    | -----------
`privateKey` | string  | Is a secret number that allows bitcoins to be spent, so be careful when handling it!
`addressTo`  | string  | It is a string that represents the public address of the wallet that you want to send the amount.
`value`      | integer | The value received in this transaction, in satoshis.


```json
{
  "id": "9b04e5034e547e0e47291488a2986e5120b0dd38e01541f7ee71136d2a676877",
  "fee": 13700,
  "transactionInput": [
    {
      "address": "mjDaJzEDCjiS86jJWmpn38nGe2A9N7EStd",
      "value": 41700
    }
  ],
  "transactionOutput": [
    {
      "address": "muwAf337HUDpuajeA2yERod4bPZyWpcqbd",
      "value": 1000
    },
    {
      "address": "mjDaJzEDCjiS86jJWmpn38nGe2A9N7EStd",
      "value": 27000
    }
  ]
}
```

### HTTP Response

A transaction is not considered confirmed until: (1) it is part of a block in the longest fork, and (2) at least 5 blocks follow it in the longest fork. In this case we say that the transaction has “6 confirmations”. This gives the network time to come to an agreed-upon the ordering of the blocks. 

Attribute           | Type    | Description
---------           | ----    | -----------
`id`                | string  | Is a string representing the hex-encoded transaction hash.
`fee`               | integer | The total number of fees in satoshis, collected by miners in this transaction.
`transactionInput`  | array[[TransactionInput](#transactioninput)]   | Array of Wallets that spend some amount in this transaction.
`transactionOutput` | array[[TransactionOutput](#transactionoutput)] | Array of Wallets that received some amount in this transaction.

#### On the right side, you will find an example of the object returned in the response you will get from the server.






