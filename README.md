# Apus

Documentação da plataforma de pagamento Apus. 

## Principais recursos

* [x] Pagamentos por cartão.
* [x] Pagamentos recorrentes.
* [x] Cancelar pagamento.
* [ ] Consulta de pagamentos.
* [x] Recarga de criptomoeda.

<hr>

## Blockchains suportadas

| Blockchain  | Value                  | Recorrente |
|-------------|------------------------|------------|
| BTC         | Blockchain::BTC        | Sim        |
| DCR         | Blockchain::DCR        | Sim        |
| ETH         | Blockchain::ETH        | Sim        |
| LTC         | Blockchain::LTC        | Sim        |

## Periodos suportados

| Period           | Value              |
|------------------|--------------------|
| Day              | Period::DAY        |
| Week             | Period::WEEK       |
| Month            | Period::MONTH      |
| Year             | Period::YEAR       |

<hr>

## Pagamentos por cartão.

Pagamentos utilizando número do cartão e senha

### Requisição

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
 
### Resposta

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

## Pagamentos recorrentes.

Pagamentos utilizando número do cartão e senha de forma recorrete.

### Requisição

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
 
### Resposta

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

## Cancelar pagamento.

Cancelar pagamento.

### Requisição

> DELETE https://api.apus.exchange/v1/checkout/

```js
{
  "txid": "d5a82f2e8469b1d30a98cbca29c40cb732c46c6b19ab729e1785806237417153",
  "password": "*******",
  "apikey": "6ZS6aF3FBnu5wEQZKsN3jbGCxUoszwDaUv89IU"
}
```
 
### Resposta

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

## Consulta de pagamentos.

Consultar pagamentos.

### Requisição

> GET https://api.apus.exchange/v1/checkout/

```js
{
}
```
 
### Resposta

```js
{
}
```

<hr>

## Recarga de criptomoeda.

Recarga de cartão com saldo de criptomoedas do comerciante.

### Requisição

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
 
### Resposta

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
