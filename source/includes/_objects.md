# Objects

This section provides a comprehensive reference for Objects in the API. For each Object there's a description and a link to a API endpoint.

<aside class="notice">
Objects sometimes contain attributes that are <b>optional.</b> These are always noted in the <b>description</b>. In these cases, the Object may not be guaranteed to include that attribute in its response.
</aside>


## AddressFrom

A AddressFrom represents an input consumed within a transaction. Generally returned and used with [Transaction Endpoint](#transaction-endpoint) and [Create Transaction Endpoint](#create-transaction-endpoint).

Attribute         | Type      | Description
---------         | ----      | -----------
**address** | _string_  | Is a string representing the address of a wallet.
**value**   | _integer_ | The value being spent in this transaction.


## AddressTo

A AddressTo represents an output created by a transaction. Generally returned and used with [Transaction Endpoint](#transaction-endpoint) and [Create Transaction Endpoint](#create-transaction-endpoint).

Attribute         | Type      | Description
---------         | ----      | -----------
**address** | _string_  | Is a string representing the address of a wallet.
**value**   | _integer_ | The value received in this transaction, in satoshis.


## TransactionsReference

A TransactionsReference object represents summarized data about a transaction. Generally returned and used with the [Wallet Endpoint](#wallet-endpoint).

Attribute         | Type      | Description
---------         | ----      | -----------
**transactionId** | _string_  | Is a string representing the hex-encoded transaction hash.
**confirmations** | _integer_ | Number of subsequent blocks, including the block the transaction is in. Unconfirmed transactions have 0 confirmations.
**value**         | _integer_ | The value transferred by this transaction in satoshis.
**blockHeight**   | _integer_ | Height of the block that contains this transaction. If it's unconfirmed, this will equal -1.
