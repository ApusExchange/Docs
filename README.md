# Apus

Documentation of the payment platform Apus.

## Main features

* [x] Payments by card.
* [x] Recurring payments.
* [x] Cancel payment.
* [ ] Consult payments.
* [x] Cryptocurrency recharge.

<hr>

## Message table

| Code  | Message                             | Description                                                  |
|-------|-------------------------------------|--------------------------------------------------------------|
| 001   | Invalid parameters                  | Some parameter sent in the body is invalid or missing        |
| 002   | Failed to connect to the database   | Technical problem connecting to the database                 |
| 003   | Database operation failed           | Some internal operation with database failed                 |
| 004   | API key not found                   | API key is incorrect or not generated correctly              |
| 005   | Error checking balance              | Failed to verify account balance in blockchain               |
| 006   | Insufficient funds                  | Wallet balance is insufficient for transaction + fees        |
| 007   | Failed to store transaction         | Internal failure to save transaction                         |
| 008   | Failed to fetch buyer               | Could not find buyer's registration                          |
| 009   | Failed to fetch merchant            | Could not find merchant's registration                       |
| 010   | Transaction not approved            | Transaction can not be approved                              |
| 011   | Module not available                | Module (blockchain) is not implemented                       |
| 012   | Invalid password                    | Password is invalid                                          |
| 013   | Buyer does not have wallet          | Buyer does not have the wallet of blockchain informed        |
| 014   | Merchant does not have wallet       | Merchant does not have the wallet of blockchain informed     |
| 015   | Failed to send email                | Internal failure to send payment receipt email               |
| 016   | Approved transaction                | Everything went well and the transaction was approved        |

## Blockchains supported

| Blockchain  | Value                  | Recorrente |
|-------------|------------------------|------------|
| BTC         | Blockchain::BTC        | Sim        |
| DCR         | Blockchain::DCR        | Sim        |
| ETH         | Blockchain::ETH        | Sim        |
| LTC         | Blockchain::LTC        | Sim        |

## Periods supported

| Period           | Value              |
|------------------|--------------------|
| Day              | Period::DAY        |
| Week             | Period::WEEK       |
| Month            | Period::MONTH      |
| Year             | Period::YEAR       |

<hr>

## Payments by card.

Payments using card number and password

### Request

> POST https://api.apus.exchange/v1/checkout/

```js
{
  "pan": "0000111122223333",
  "password": "*******",
  "blockchain": Blockchain::BTC,
  "amount": 10.00,
  "currency": "BRL",
  "apikey": "6ZS6aF3FBnu5wEQZKsN3jbGCxUoszwDaUv89IU"
}
```
 
### Response

```js
{
    "code": "016",
    "message": "Approved transaction",
    "txId": "74fee55a9155e2e49f34a6d0c62d3b72fd1b0f1824b68185ccf3bc8b74185158",
    "timestamp": 1536427020652,
    "date": "2018-09-08T14:17:00-03:00",
    "coin": {
        "name": "LTC",
        "amount": "0.04413179",
        "fee": 0.00054
    },
    "currency": {
        "name": "BRL",
        "amount": "10.00"
    },
    "buyer": "Name of buyer"
}
```

<hr>

## Recurring payments.

Payments using card number and password on a recurring basis.

### Request

> POST https://api.apus.exchange/v1/checkout/

```js
{
  "pan": "0000111122223333",
  "password": "*******",
  "blockchain": Blockchain::BTC,
  "amount": 10.00,
  "currency": "BRL",
  "period": Period::MONTH,
  "frequency": 12,
  "apikey": "6ZS6aF3FBnu5wEQZKsN3jbGCxUoszwDaUv89IU"
}
```
 
### Response

```js
{
    "code": 001,
    "message": "Pagamento efetuado com sucesso!",
    "txid": "d5a82f2e8469b1d30a98cbca29c40cb732c46c6b19ab729e1785806237417153",
    "data": {
        ?: ?
    }
}
```

<hr>

## Cancel payment.

Cancel payment.

### Request

> DELETE https://api.apus.exchange/v1/checkout/

```js
{
  "txid": "d5a82f2e8469b1d30a98cbca29c40cb732c46c6b19ab729e1785806237417153",
  "password": "*******",
  "apikey": "6ZS6aF3FBnu5wEQZKsN3jbGCxUoszwDaUv89IU"
}
```
 
### Response

```js
{
    "code": 003,
    "message": "Pagamento cancelado com sucesso!",
    "txid": "CAF8F464F4AAEF047028B9BCA1CD17510BD93902045FF0F1407DFFC4AC270270",
    "data": {
        ?: ?
    }
}
```

<hr>

## Consult payments.

Consult payments.

### Request

> GET https://api.apus.exchange/v1/checkout/

```js
{
}
```
 
### Response

```js
{
}
```

<hr>

## Cryptocurrency recharge.

Refill card with merchant's cryptocurrency balance.

### Request

> POST https://api.apus.exchange/v1/checkin/

```js
{
  "pan": "0000111122223333",
  "password": "*******",
  "blockchain": Blockchain::BTC,
  "amount": 10.00,
  "currency": "BRL",
  "apikey": "6ZS6aF3FBnu5wEQZKsN3jbGCxUoszwDaUv89IU"
}
```
 
### Response

```js
{
    "code": 002,
    "message": "Recarga efetuada com sucesso!",
    "txid": "d5a82f2e8469b1d30a98cbca29c40cb732c46c6b19ab729e1785806237417153",
    "data": {
        ?: ?
    }
}
```
