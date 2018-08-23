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

| Blockchain       | Value                  | Recorrente |
|------------------|------------------------|------------|
| Bitcoin          | Blockchain::BTC        | Sim        |
| Decred           | Blockchain::DCR        | Sim        |
| Ethereum         | Blockchain::ETH        | Sim        |
| Litecoin         | Blockchain::LTC        | Sim        |

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
    "code": 001,
    "message": "Pagamento efetuado com sucesso!",
    "txid": "d5a82f2e8469b1d30a98cbca29c40cb732c46c6b19ab729e1785806237417153",
    "data": {
        ?: ?
    }
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
