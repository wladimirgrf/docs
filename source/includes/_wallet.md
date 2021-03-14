# Wallet API

Bitchain's Wallet API allows you to look up information about public addresses on the blockchain, generate key pairs with corresponding addresses. If you're new to blockchains, you can think of public addresses as similar to bank account numbers in a traditional ledger. The biggest differences:

- Anyone can generate a public address themselves (through [ECDSA](https://en.wikipedia.org/wiki/EllipticCurveDigitalSignatureAlgorithm). in Bitcoin). No single authority is needed to generate new addresses.

- Public addresses are significantly more lightweight. Consequently, and unlike traditional bank accounts, you can (and should) generate new addresses for every transaction.

## Wallet Endpoint

```shell
curl "https://testnet.bitchain.network/wallets/tb1qe8ayn3j3adu72496v48v5cvj40gqpjz09uh800"
```

The default Wallet Endpoint strikes a balance between speed of response and data on Addresses. It returns more information about an address' transactions than the Address Balance Endpoint but doesn't return full transaction information.

### HTTP Request

<div class="endpoint">
  <i>GET</i>
  <span>https://testnet.bitchain.network/wallets/:address</span>
</div>

### URL Parameters

Parameter   | Description
---------   | -----------
`address` | The address is a string representing the public address you're interested in querying.

`Example: tb1qe8ayn3j3adu72496v48v5cvj40gqpjz09uh800`

```json
{
  "address": "tb1qe8ayn3j3adu72496v48v5cvj40gqpjz09uh800",
  "balance": 30000,
  "confirmedBalance": 30000,
  "unconfirmedBalance": 0,
  "referenceTransactions": [
    {
      "transactionId": "d8db85b8aa834bab65c59eac0159ad166c3b89e09a06520412c9821e71222f52",
      "confirmations": -1,
      "value": 10000,
      "blockHeight": 1938604
    },
    {
      "transactionId": "a3fe0c54b470064411db65497a658d5d96478eb3ec39b47e556974091b5b9122",
      "confirmations": -1,
      "value": 1000000,
      "blockHeight": 1938604
    },
    {
      "transactionId": "5a8a0a2930a29efa4b6e6972b6ab093bb406b51af90e1bcb230e2e5de7217b13",
      "confirmations": -1,
      "value": 100000,
      "blockHeight": 1938566
    },
    {
      "transactionId": "a64e39a56f4b0dd31734e774d9bc98713b719f6364212d84d76c50212c1058d5",
      "confirmations": -1,
      "value": 10000,
      "blockHeight": 1938566
    },
    {
      "transactionId": "85fd8379a361f89dc173eae0f8c324533702602062546a10490fd8bfc1b048fb",
      "confirmations": -1,
      "value": 10000,
      "blockHeight": 1938566
    }
  ]
}
```

### HTTP Response

This response represents a public address on a blockchain, and contains information about the state of balances and transactions related to this address.

Attribute                 | Type       | Description
---------                 | ----       | -----------
`address`               | string   | Is a string representing the address of a wallet.
`balance`               | integer  | Total balance of satoshis, including confirmed and unconfirmed transactions, for this address.
`confirmedBalance`      | integer  | Balance of confirmed satoshis on this address, but only for transactions that have been included into a block.
`unconfirmedBalance`    | integer  | Balance of unconfirmed satoshis on this address. Can be negative (if unconfirmed transactions are just spending outputs). Only unconfirmed transactions (haven't made it into a block) are included.
`transactionsReference` | array[[TransactionsReference](#transactionsreference)] | **Optional** Array of transaction history for this address.

#### On the right side, you will find an example of the object returned in the response you will get from the server.


## Create Wallet Endpoint

```shell
curl -X POST "https://testnet.bitchain.network/wallets/create"
```

The Create Wallet endpoint allows you to generate private-public key-pairs along with an associated public address. 
No information is required with this POST request.

<aside class="warning">Always use HTTPS for Wallet Generation requests. Otherwise, your generated private keys will be sent over insecure channels and could be MITM'd.</aside>

### HTTP Request

<div class="endpoint">
  <i>POST</i>
  <span>https://testnet.bitchain.network/wallets/create</span>
</div>

```json
{
  "publicAddress": "mffzq5WLcJVsokpSjVgPmjPmUCK5K2UoZN",
  "privateKey": "cW33mrcvCY2YzoFegug4xfQ8U4yNEAeLRUs2z78ZwCwb4w1Fn35K"
}
```

### HTTP Response

This response represents an associated collection of public and private keys alongside their respective public address.

Attribute      | Type     | Description
---------      | ----     | -----------
`address`    | string | Is a string representing the address of a wallet.
`privateKey` | string | Is a secret number that allows bitcoins to be spent, so be careful when handling it!

#### On the right side, you will find an example of the object returned in the response you will get from the server.

