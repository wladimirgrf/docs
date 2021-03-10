# Transaction API

Bitchain's Transaction API allows you to look up information about unconfirmed transactions, query transactions based on public id (hash), create and propagate your own transactions.



## Transaction Endpoint

```shell
curl https://testnet.bitchain.network/transactions/d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53
```

```json
{
  "publicId": "d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53",
  "fee": 24547,
  "confirmations": 1194,
  "date": "2021-03-02T21:02:23.000Z",
  "addressFrom": [
    {
      "publicAddress": "tb1q3yyq37lalgq0chareur9yykgtgpqwztt5uezvz",
      "value": 78836818
    },
    {
      "publicAddress": "tb1qrgrmt8cm6n7nhqz9lexvy0rxul0xr52m2gay0u",
      "value": 71923196
    }
  ],
  "addressTo": [
    {
      "publicAddress": "mhfNudm6YDYnYkegFSjcsppucpAA8TRviD",
      "value": 100000000
    },
    {
      "publicAddress": "tb1q7zf06fvr8jq889k3v6ly2l0slxphtuka6dlmcs",
      "value": 50735467
    }
  ]
}
```

The Transaction Endpoint returns detailed information about a given transaction based on its public id (hash).


Resource          |	Method | Object
--------          | ------ | ------
/transactions/:id | GET    | [Transaction](#transaction)


### URL Parameters

Parameter | Description
--------- | -----------
**id**    | The id is a string representing the hex-encoded transaction hash you're interested in querying

Example: `d3571c42e5379ea70bce0c2c3c571018a293c5598dad4b2e0c0b7b4f0e625c53`
