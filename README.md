# [ApusPayments](https://apuspayments.com/)

ApusPayments is a plataform to make payments using criptocurrencies. 

[Documentation API](https://docs.apuspayments.com/) 

![GitHub manifest version](https://img.shields.io/github/manifest-json/v/ApusPayments/Docs.svg)

<hr>

## Main features

* [x] Payments by card.
* [x] Recurring payments.
* [x] Cancel payment.
* [x] Consult payments.
* [x] Cryptocurrency recharge.

<hr>

## Message table

| Code  | Message                             | Description                                                  |
|-------|-------------------------------------|--------------------------------------------------------------|
| 001   | Invalid parameters                  | Some parameter sent in the body is invalid or missing        |
| 002   | Failed to connect to the database   | Technical problem connecting to the database                 |
| 003   | Database operation failed           | Some internal operation with database failed                 |
| 004   | Vendor key not found                | Vendor key is incorrect or not generated correctly           |
| 005   | Error checking balance              | Failed to verify account balance in blockchain               |
| 006   | Insufficient funds                  | Wallet balance is insufficient for transaction + fees        |
| 007   | Failed to store transaction         | Internal failure to save transaction                         |
| 008   | Failed to fetch buyer               | Could not find buyer's registration                          |
| 009   | Buyer not found by PAN              | Could not find buyer's registration by PAN                   |
| 010   | Failed to fetch merchant            | Could not find merchant's registration                       |
| 011   | Transaction not approved            | Transaction can not be approved                              |
| 012   | Module not available                | Module (blockchain) is not implemented                       |
| 013   | Invalid password                    | Password is invalid                                          |
| 014   | Buyer does not have wallet          | Buyer does not have the wallet of blockchain informed        |
| 015   | Merchant does not have wallet       | Merchant does not have the wallet of blockchain informed     |
| 016   | Failed to send email                | Internal failure to send payment receipt email               |
| 017   | Approved transaction                | Everything went well and the transaction was approved        |
| 018   | Failed to store schedule            | Internal failure to save schedule                            |
| 019   | Successful payment and scheduling   | Successful made payment and save scheduling                  |
| 020   | Successful scheduling               | Successful save scheduling                                   |
| 021   | Query performed successfully        | Everything went well when querying payments                  |

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
  "vendorKey": "6ZS6aF3FBnu5wEQZKsN3jbGCxUoszwDaUv89IU"
}
```
 
### Response

```js
{
    "status": {
        "code": "017",
        "message": "Approved transaction"
    },
    "transaction": {
        "txId": "ef60f9128da76a2cf925dc7dd2d69a9452ad81131bc0ab6b79fd22f357a3327e",
        "timestamp": 1536708260759,
        "buyer": "Name of buyer"
    },
    "coin": {
        "name": "LTC",
        "amount": "0.04601453",
        "fee": 0.00054
    },
    "currency": {
        "name": "BRL",
        "amount": "10.00"
    }
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
  "vendorKey": "6ZS6aF3FBnu5wEQZKsN3jbGCxUoszwDaUv89IU"
}
```

### Response

> Schedule and pay ["execute": "true"]

```js
{
    "transaction": {
        "timestamp": 1536708242411,
        "buyer": "Name of buyer",
        "txId": "90a2217d6d45438b6d5fda485eb6920243825bdeb24eabd4e77fa1d33f15105e"
    },
    "coin": {
        "name": "LTC",
        "amount": "0.04601453",
        "fee": 0.00054
    },
    "currency": {
        "name": "BRL",
        "amount": "10.00"
    },
    "schedule": {
        "period": "M",
        "frequency": 12,
        "execute": "true",
        "id": "4e4bb526-e476-411c-98b7-aa9683766b34"
    },
    "status": {
        "code": "019",
        "message": "Successful payment and scheduling"
    }
}
```

> Only schedule ["execute": "false"]

```js
{
    "transaction": {
        "timestamp": 1536715932723,
        "buyer": "Name of buyer"
    },
    "coin": {
        "name": "LTC"
    },
    "currency": {
        "name": "BRL",
        "amount": "10.00"
    },
    "schedule": {
        "period": "M",
        "frequency": 12,
        "execute": "false",
        "id": "04388c12-c19e-4fe0-9dc1-ac668cbc4297"
    },
    "status": {
        "code": "020",
        "message": "Successful scheduling"
    }
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

> GET https://sandbox.apus.exchange/v1/checkout/:vendorKey
?txId=?
&timestamp=?
&blockchain=?
&currency=?
&coinAmount=?
&currencyAmount=?
&buyer=?
 
### Response

```js
{
    "status": {
        "code": "021",
        "message": "Query performed successfully"
    },
    "data": [
    {
        "buyer": {
            "address": "QWKKEKRbRf2XrsbdQ8Cd5cgLxY7B6CGP37",
            "userId": "43de9565-943e-49ff-b808-82d54a87199f"
        },
        "coin": {
            "amount": "0.04494037",
            "fee": 0.00054,
            "name": "LTC"
        },
        "currency": {
            "amount": 9.00,
            "name": "BRL"
        },
        "date": "2018-09-10T23:11:03-03:00",
        "id": "05e75c97-6c75-43e6-ac9f-02205707a364",
        "seller": {
            "address": "QbTaFSttxH4SfvTKoB14EKapWjk5Da5di2",
            "userId": "5f5bdaed-f82b-4b82-b3f5-1d562633da5b"
        },
        "txId": "2bf779e2a311c2629df977b0bb105879411fd71f5839972c4ed1d3278f80170f"
    },
    {
        "buyer": {
            "address": "QWKKEKRbRf2XrsbdQ8Cd5cgLxY7B6CGP37",
            "userId": "43de9565-943e-49ff-b808-82d54a87199f"
        },
        "coin": {
            "amount": "0.04494557",
            "fee": 0.00054,
            "name": "LTC"
        },
        "currency": {
            "amount": 11.00,
            "name": "BRL"
        },
        "date": "2018-09-10T22:59:38-03:00",
        "id": "0ae33f54-d66f-4751-8773-61c0f5f09357",
        "seller": {
            "address": "QbTaFSttxH4SfvTKoB14EKapWjk5Da5di2",
            "userId": "5f5bdaed-f82b-4b82-b3f5-1d562633da5b"
        },
        "txId": "d18b42ec51e18509382ebfd5b9ca06b7df0e06403452fe65a39665a4cebe5b52"
    }
    ...
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
  "blockchain": Blockchain::LTC,
  "amount": 10.00,
  "currency": "BRL",
  "vendorKey": "6ZS6aF3FBnu5wEQZKsN3jbGCxUoszwDaUv89IU"
}
```
 
### Response

```js
{
    "status": {
        "code": "017",
        "message": "Approved transaction"
    },
    "transaction": {
        "txId": "ef60f9128da76a2cf925dc7dd2d69a9452ad81131bc0ab6b79fd22f357a3327e",
        "timestamp": 1536708260759,
        "buyer": "Name of buyer"
    },
    "coin": {
        "name": "LTC",
        "amount": "0.04601453",
        "fee": 0.00054
    },
    "currency": {
        "name": "BRL",
        "amount": "10.00"
    }
}
```