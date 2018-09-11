# Apus

Documentation of the payment platform Apus.

## Main features

* [x] Payments by card.
* [x] Recurring payments.
* [ ] Cancel payment.
* [ ] Consult payments.
* [ ] Cryptocurrency recharge.

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

## Currencies supported

| Value     | Currency             | Description          |
|-----------|----------------------|----------------------|
| BLR       | Currency::BLR        | Brazilian real       |
| CAD       | Currency::CAD        | Canadian dollar      |
| CNY       | Currency::CNY        | China yuan renminbi  |
| EUR       | Currency::EUR        | Euro                 |
| JPY       | Currency::JPY        | Japanese yen         |
| USD       | Currency::USD        | United States dollar |

## Blockchains supported

| Value       | Blockchain             | Recurrent? |
|-------------|------------------------|------------|
| BTC         | Blockchain::BTC        | Yes        |
| DCR         | Blockchain::DCR        | Yes        |
| ETH         | Blockchain::ETH        | Yes        |
| LTC         | Blockchain::LTC        | Yes        |

## Periods supported

| Value   | Period             | Description           |
|---------|--------------------|-----------------------|
| D       | Period::DAY        | Daily transactions    |
| W       | Period::WEEK       | Weekly transactions   |
| M       | Period::MONTH      | Monthly transactions  |
| Y       | Period::YEAR       | Annual transactions   |

<hr>

## Payments by card.

Payments using card number and password

### Request

> POST https://sandbox.apus.exchange/v1/checkout/

```js
{
  "pan": "0000111122223333",
  "password": "*******",
  "blockchain": Blockchain::LTC,
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

> POST https://sandbox.apus.exchange/v1/checkout/recurrent

```js
{
  "pan": "0000111122223333",
  "password": "*******",
  "blockchain": Blockchain::LTC,
  "amount": 10.00,
  "currency": "BRL",
  "period": Period::MONTH,
  "frequency": 12,
  "execute": false|true,
  "apikey": "6ZS6aF3FBnu5wEQZKsN3jbGCxUoszwDaUv89IU"
}
```

### Response

#### Schedule and pay ("execute": "true")

```js
{
    "code": "017",
    "message": "Successful payment and scheduling",
    "id": "bbee6d15-ecc9-489e-9611-274ae7acefd3"
    "txId": "2bf779e2a311c2629df977b0bb105879411fd71f5839972c4ed1d3278f80170f",
    "timestamp": 1536631861766,
    "date": "2018-09-10T23:11:01-03:00",
    "coin": {
        "name": "LTC",
        "amount": "0.04494037",
        "fee": 0.00054
    },
    "currency": {
        "name": "BRL",
        "amount": "10.00"
    },
    "schedule": {
        "period": "M",
        "frequency": "12",
        "execute": "true"
    },
    "buyer": "Name of buyer",
}
```

#### Only schedule ("execute": "false")

```js
{
    "code": "018",
    "message": "Successful scheduling",
    "id": "1a19a4ee-7578-49f7-a379-1b5103e6ace6"
    "timestamp": 1536631964775,
    "date": "2018-09-10T23:12:44-03:00",
    "coin": {
        "name": "LTC"
    },
    "currency": {
        "name": "BRL",
        "amount": "10.00"
    },
    "schedule": {
        "period": "M",
        "frequency": "12",
        "execute": "false"
    },
    "buyer": "Name of buyer",
}
```

<hr>

## Cancel payment.

Cancel payment.

### Request

> DELETE https://sandbox.apus.exchange/v1/checkout/

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

> GET https://sandbox.apus.exchange/v1/checkout/

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

> POST https://sandbox.apus.exchange/v1/checkin/

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
