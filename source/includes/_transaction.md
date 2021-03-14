# Transaction API

Transactions are grouped into blocks and about every 10 minutes, a new block of transactions is sent out, becoming part of the transaction log (Blockchain), which indicates the transaction has been made (more-or-less) official. Once a transaction has been successfully mined in the blockchain, you can say that you transferred a certain amount of BTC to another address.

Bitchain's Transaction API allows you to look up information about unconfirmed transactions, query transactions based on their id (hash), create and propagate your own transactions. 

## Transaction Endpoint

```shell
curl "https://testnet.bitchain.network/transactions/d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53"
```

The Transaction Endpoint returns detailed information about a given transaction based on its public id (hash).

### HTTP Request

<div class="endpoint">
  <i>GET</i>
  <span>https://testnet.bitchain.network/transactions/:id</span>
</div>

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
  "addressFrom": [
    {
      "address": "tb1q3yyq37lalgq0chareur9yykgtgpqwztt5uezvz",
      "value": 78836818
    },
    {
      "address": "tb1qrgrmt8cm6n7nhqz9lexvy0rxul0xr52m2gay0u",
      "value": 71923196
    }
  ],
  "addressTo": [
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

Attribute         | Type      | Description
---------         | ----      | -----------
`id`            | string  | Is a string representing the hex-encoded transaction hash.
`fee`           | integer | The total number of fees in satoshis, collected by miners in this transaction.
`confirmations` | integer | Number of subsequent blocks, including the block the transaction is in. Unconfirmed transactions have 0 confirmations.
`date`          | string  | Time this transaction was received by the Blockchain provider.
`addressFrom`   | array[[AddressFrom](#addressfrom)] | Array of Wallets that spend some amount in this transaction.
`addressTo`     | array[[AddressTo](#addressto)]     | Array of Wallets that received some amount in this transaction.

#### On the right side, you will find an example of the object returned in the response you will get from the server.


## Transaction Fee Endpoint

```shell
curl -d '{"addressFrom": "muwAf337HUDpuajeA2yERod4bPZyWpcqbd","addressTo": "mjDaJzEDCjiS86jJWmpn38nGe2A9N7EStd","value": 10000}' "https://testnet.bitchain.network/transactions/fee"
```

The Transaction Fee Endpoint returns the estimated mining fee amount (in satoshis) for a transaction, based on the addresses and value involved.

### HTTP Request

<div class="endpoint">
  <i>POST</i>
  <span>https://testnet.bitchain.network/transactions/fee</span>
</div>

### Body

Attribute       | Type      | Description
---------       | ----      | -----------
`addressFrom` | string  | It is a string that represents the public address of a wallet that has a value to spend.
`addressTo`   | string  | It is a string that represents the public address of the wallet that you want to send the amount.
`value`       | integer | The value received in this transaction, in satoshis.

```json
{
  "transactionEstimatedFee": 15200
}
```

### HTTP Response

Attribute                   | Type      | Description
---------                   | ----      | -----------
`transactionEstimatedFee` | integer | The estimated mining fee amount for the transaction, in satoshis.

#### On the right side, you will find an example of the object returned in the response you will get from the server.


## Create Transaction Endpoint

```shell
curl -d '{"privateKey": "cW33mrcvCY2YzoFegug4xfQ8U4yNEAeLRUs2z78ZwCwb4w1Fn35K","addressTo": "muwAf337HUDpuajeA2yERod4bPZyWpcqbd","value": 1000}' "https://testnet.bitchain.network/transactions/create"
```

Using Bitchain's API, you can push transactions to blockchain. 

<aside class="notice">
For security reasons, we never take possession of your private keys.
</aside>

### HTTP Request

<div class="endpoint">
  <i>POST</i>
  <span>https://testnet.bitchain.network/transactions/create</span>
</div>

### Body

Attribute      | Type      | Description
---------      | ----      | -----------
`privateKey` | string  | Is a secret number that allows bitcoins to be spent, so be careful when handling it!
`addressTo`  | string  | It is a string that represents the public address of the wallet that you want to send the amount.
`value`      | integer | The value received in this transaction, in satoshis.


```json
{
  "id": "ab0eee27325d5fad40431f52294edf2c09258ce85fd40a8283d6a64c6d6ddbde",
  "fee": 15200,
  "addressFrom": [
    {
      "address": "muwAf337HUDpuajeA2yERod4bPZyWpcqbd",
      "value": 2750343
    }
  ],
  "addressTo": [
    {
      "address": "muwAf337HUDpuajeA2yERod4bPZyWpcqbd",
      "value": 1000
    },
    {
      "address": "muwAf337HUDpuajeA2yERod4bPZyWpcqbd",
      "value": 2734143
    }
  ]
}
```

### HTTP Response

A transaction is not considered confirmed until: (1) it is part of a block in the longest fork, and (2) at least 5 blocks follow it in the longest fork. In this case we say that the transaction has “6 confirmations”. This gives the network time to come to an agreed-upon the ordering of the blocks. 

Attribute         | Type      | Description
---------         | ----      | -----------
`id`            | string  | Is a string representing the hex-encoded transaction hash.
`fee`           | integer | The total number of fees in satoshis, collected by miners in this transaction.
`addressFrom`   | array[[AddressFrom](#addressfrom)] | Array of Wallets that spend some amount in this transaction.
`addressTo`     | array[[AddressTo](#addressto)]     | Array of Wallets that received some amount in this transaction.

#### On the right side, you will find an example of the object returned in the response you will get from the server.






