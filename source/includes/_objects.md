# Objects

This section provides a comprehensive reference for Objects in the API. For each Object there's a description and a link to a API endpoint.

<aside class="notice">
Objects sometimes contain attributes that are <b>optional.</b> These are always noted in the <b>description</b>. In these cases, the Object may not be guaranteed to include that attribute in its response.
</aside>

## Address

An Address represents a public address on a blockchain, and contains information about the state of balances and transactions related to this address. Typically returned from the [Wallet Endpoint](#wallet-endpoint).


Attribute                 | Type       | Description
---------                 | ----       | -----------
**publicAddress**         | _string_   | The requested address.
**balance**               | _integer_  | Total balance of satoshis, including confirmed and unconfirmed transactions, for this address.
**confirmedBalance**      | _integer_  | Balance of confirmed satoshis on this address, but only for transactions that have been included into a block.
**unconfirmedBalance**    | _integer_  | Balance of unconfirmed satoshis on this address. Can be negative (if unconfirmed transactions are just spending outputs). Only unconfirmed transactions (haven't made it into a block) are included.
**transactionsReference** | _array[[TransactionsReference](#transactionsreference)]_ | **Optional** Array of transaction history for this address.


## Wallet

An Wallet represents an associated collection of public and private keys alongside their respective public address. Generally returned and used with the [Generate Wallet Endpoint](#generate-wallet-endpoint).

Attribute         | Type     | Description
---------         | ----     | -----------
**publicAddress** | _string_ | Is a string representing the public address of a wallet.
**privateKey**    | _string_ | Is a secret number that allows bitcoins to be spent, so be careful when handling it!


## AddressFrom

A AddressFrom represents an input consumed within a transaction. Typically found within an array in a [Transaction](#transaction).

Attribute         | Type      | Description
---------         | ----      | -----------
**publicAddress** | _string_  | Is a string representing the public address of a wallet.
**value**         | _integer_ | The value being spent in this transaction.

## AddressTo

A AddressTo represents an output created by a transaction. Typically found within an array in a [Transaction](#transaction).

Attribute         | Type      | Description
---------         | ----      | -----------
**publicAddress** | _string_  | Is a string representing the public address of a wallet.
**value**         | _integer_ | The value received in this transaction, in satoshis.

## Transaction

A Transaction represents the current state of a particular transaction from either a Block within a Blockchain, or an unconfirmed transaction that has yet to be included in a Block. Typically returned from the [Transaction Endpoint](#transaction-endpoint).

Attribute         | Type      | Description
---------         | ----      | -----------
**publicId**      | _string_  | The hash of the transaction.
**fee**           | _integer_ | The total number of fees in satoshis, collected by miners in this transaction.
**confirmations** | _integer_ | Number of subsequent blocks, including the block the transaction is in. Unconfirmed transactions have 0 confirmations.
**date**          | _string_  | Time this transaction was received by the Blockchain provider.
**addressFrom**   | _array[[AddressFrom](#addressfrom)]_ | Array of Wallets that spend some amount in this transaction.
**addressTo**     | _array[[AddressTo](#addressto)]_     | Array of Wallets that received some amount in this transaction.

## TransactionsReference

A TransactionsReference object represents summarized data about a transaction. Typically found in an array within an [Address](#address) object.


Attribute         | Type      | Description
---------         | ----      | -----------
**transactionId** | _string_  | The hash of the transaction.
**confirmations** | _integer_ | Number of subsequent blocks, including the block the transaction is in. Unconfirmed transactions have 0 confirmations.
**value**         | _integer_ | The value transferred by this transaction in satoshis.
**blockHeight**   | _integer_ | Height of the block that contains this transaction. If it's unconfirmed, this will equal -1.
