# CS30 SmartContract General API Information


### Endpoints
--- 

`POST` | `https://api-smartcontract.cse30.io/api/v1`

By default, you need access API Key and API Secret to use apis from api-smartcontract.cse30.io.
Please try to sign in/ signup  on https//smartcontrart.cse30.io to get an apiKey and apiSecret

Key | Value
------------ | ------------
apikey | `your API Key`.
apisecret | `your API Secret`.

>Example:

```
curl --location --request POST "http://api-smartcontract.cse30.io/wallets" \
  --header "Content-Type: application/json" \
  --header "apikey: `your APIKey`" \
  --header "apisecret: `your API Secret`" \
  --data "{
    \"tokenAddress\": \"d2e7d058d6429a7113e26b3c3c7acd6d3d32eccf\",
}"
```
### Restfull APIs
---
 - [Create a token wallet](#create_wallet)
 - [Get token wallet balance](#get_balance)
 - [Transfer tokens](#transfer)
 - [Get transaction by txid](#get_transaction_by_txid)
 - [Get transactions by address](#get_transactions_by_address)
 - [Get block by hash](#get_block_by_hash) - Comming soon
  
 ---
# create_wallet

``` POST /wallets/ ```

**Parameters**

``` Object ```
 - tokenAddress - ``` String ```
 
**Returns**

``` Object ``` - A block object
 - address - ``` String ```
 - privateKey - ``` String ```
 - publicKey - ``` String ```
 - symbol - ``` String ```

**Example**

Request
```
  {
    "tokenAddress": "d2e7d058d6429a7113e26b3c3c7acd6d3d32eccf",
  }
```
  
Result
```
{
    "address": "cs90616e9e12be459b379b600c38ea861ecb4c605a0",
    "privateKey": "589ac84a84****ef9093ce091aafdeac1a****b20a3bab847004a6f839b9****",
    "publicKey": "31b4417d0f68c****6677699c33ab33f768664e****1f88afdf3196aa6384a****cd7a820ecf9ccc5cfa2b5b6c****4e63015d4a1f18aaf0c****8d64a0fd9a6",
    "symbol": "cs9"
  }
```
---

# transfer
``` POST /wallets/send ```

Transfer amount to another address

**Parameters**

``` Object ```
- privateKey - ``` String ```
- tokenAddress - ``` String ```
- amount - ``` Number ```
- toAddress - ``` String ```

**Returns**

``` Object ```
- txid - ``` String ```

**Example**

Request
```
  {
    "privateKey": "31b4417d0f68c****6677699c33ab33f768664e****1f88afdf3196aa6384a****cd7a820ecf9ccc5cfa2b5b6c****4e63015d4a1f18aaf0c****8d64a0fd9a6",
    "tokenAddress": "d2e7d058d6429a7113e26b3c3c7acd6d3d32eccf",
    "amount": 100,
    "toAddress": "cs90616e9e12be459b379b600c38ea861ecb4c60000"
  }
```
Result
```
  {
    "txid": "a20af5776a30****f239b146207b4cb7be41e29e5****ec29192677e9ddc5bf7",
  }
```
---

# get_transaction_by_txid

``` POST /transactions/txId ```

**Parameters**
- TxId

**Returns**

``` Object ```
- amount - ``` String ```
- txId - ``` String ```
- tokenAddress - ``` String ```
- symbol - ``` String ```
- blockHash - ``` String ```
- toAddress - ``` String ```
- fromAddress - ``` String ```
- status - ``` String ```
- feeNetwork - ``` Number ``` 
- feeToken - ``` Number ```
- createdAt - ``` Number ```

**Example**

Request
```
  {
    "txId":"a20af5776a30bcd9f239b146207b4cb7be41e29e58c44ec29192677e9ddc5bf7"
  }
```
Result
```
  {
    "amount": "100.000000",
    "fromAddress": "cs9d0b4651a48376a1492f96d2fdc2629e8af97b4ef",
    "toAddress": "cs9fd2c1547883980a70b69ee044d36d009f96779d1",
    "txId": "a20af5776a30bcd9f239b146207b4cb7be41e29e58c44ec29192677e9ddc5bf7",
    "blockHash": "263edb88e32ac18ec080ae64a629f12aff3c8a65778270063c769314ee8407c8",
    "tokenAddress": "d2e7d058d6429a7113e26b3c3c7acd6d3d32eccf",
    "symbol": "CS9",
    "feeNetwork": "0.15",
    "feeToken": "0.15",
    "type": 1,
    "status": "SUCCESS",
    "createdAt": 1612310400000
  }
```
---

# get_transactions_by_address

``` GET /transactions ```

Return transactions by address

**Parameters**
- address
- type - ``` ALL|RECEIVE|SEND ```
- page
- limit

**Returns**

``` Object ```
- amount - ``` String ```
- txId - ``` String ```
- tokenAddress - ``` String ```
- symbol - ``` String ```
- blockHash - ``` String ```
- toAddress - ``` String ```
- fromAddress - ``` String ```
- status - ``` String ```
- feeNetwork - ``` Number ``` 
- feeToken - ``` Number ```
- createdAt - ``` Number ```

**Example**

Request
```
 GET /transactions?address=cs9d0b4651a48376a1492f96d2fdc2629e8af97b4ef&type=ALL&limit=10&page=1
```
Result
  ```
    {
      docs: [
        {
          "amount": "100.000000",
          "fromAddress": "cs9d0b4651a48376a1492f96d2fdc2629e8af97b4ef",
          "toAddress": "cs9fd2c1547883980a70b69ee044d36d009f96779d1",
          "txId": "a20af5776a30bcd9f239b146207b4cb7be41e29e58c44ec29192677e9ddc5bf7",
          "blockHash": "263edb88e32ac18ec080ae64a629f12aff3c8a65778270063c769314ee8407c8",
          "tokenAddress": "d2e7d058d6429a7113e26b3c3c7acd6d3d32eccf",
          "symbol": "CS9",
          "feeNetwork": "0.15",
          "feeToken": "0.15",
          "type": 1,
          "status": "SUCCESS",
          "createdAt": 1612310400000
        }
      ],
      "totalDocs": 0,
      "limit": 10,
      "totalPages": 1,
      "page": 1,
    }
  ```
---

### Webhook Notification Events

CS30 SmartContract will send webhook events whenever you successfully receive a payment.

# `Wallet Deposited Success`

**Event Type:** ``` WALLET_DEPOSITED_SUCCESS ```

**Payload:**
```
{
   "type":"WALLET_DEPOSITED_SUCCESS",
   "data":{
      "address":"cs9fd2c1547883980a70b69ee044d36d009f96779d1",
      "amount":"100.00000",
      "rawTransaction":{
         "amount": "100.000000",
         "fromAddress": "cs9d0b4651a48376a1492f96d2fdc2629e8af97b4ef",
         "toAddress": "cs9fd2c1547883980a70b69ee044d36d009f96779d1",
         "txId": "a20af5776a30bcd9f239b146207b4cb7be41e29e58c44ec29192677e9ddc5bf7",
         "blockHash": "263edb88e32ac18ec080ae64a629f12aff3c8a65778270063c769314ee8407c8",
         "tokenAddress": "d2e7d058d6429a7113e26b3c3c7acd6d3d32eccf",
         "symbol": "CS9",
         "feeNetwork": "0.15",
         "feeToken": "0.15",
         "type": 1,
         "status": "SUCCESS",
         "createdAt": 1612310400000
      }
   }
}
```
---

# `Wallet Withdrawal Success`

**Event Type:** ``` WALLET_WITHDRAWAL_SUCCESS ```

**Payload:**
```
{
   "type":"WALLET_WITHDRAWAL_SUCCESS",
   "data":{
      "address":"cs9d0b4651a48376a1492f96d2fdc2629e8af97b4ef",
      "amount":"100.00000",
      "rawTransaction":{
         "amount": "100.000000",
         "fromAddress": "cs9d0b4651a48376a1492f96d2fdc2629e8af97b4ef",
         "toAddress": "cs9fd2c1547883980a70b69ee044d36d009f96779d1",
         "txId": "a20af5776a30bcd9f239b146207b4cb7be41e29e58c44ec29192677e9ddc5bf7",
         "blockHash": "263edb88e32ac18ec080ae64a629f12aff3c8a65778270063c769314ee8407c8",
         "tokenAddress": "d2e7d058d6429a7113e26b3c3c7acd6d3d32eccf",
         "symbol": "CS9",
         "feeNetwork": "0.15",
         "feeToken": "0.15",
         "type": 1,
         "status": "SUCCESS",
         "createdAt": 1612310400000
      }
   }
}
```
