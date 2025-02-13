---
sidebarDepth: 4
---

# Onroad
:::tip Maintainer
[vite-crzn](https://github.com/vite-crzn)
:::

## On-road Module

The definition of "OnRoad" is actually used to describe the state of a transaction. It specifically refers to request transaction which has not been received and has open, pending receive status. The BlockType of on-road transaction is usually represented as 1, 2, 3 or 6, which in turn correspond to 'send a transaction to create a contract', 'make a transfer or call contract', 'send a transaction to get reward' and 'send a transaction to refund.'

This concept is often confusing with unconfirmed transactions. The latter are actually transactions not snapshoted. All transactions are stored in ledger, including request transactions and respond transactions, while the terms "onroad" and "unconfirmed" are just used to describe the different states of transactions. All onroad are request transactions, while an unconfirmed transaction can be either request or respond.


## onroad_getOnroadBlocksByAddress <Badge text="public"/>

Return all open transactions waiting to be received by specified account

- **Parameters**:

  * `Address`: Account address
  * `uint64`: Page index
  * `uint64`: Page size up to 256

- **Return**:

  * `[]AccountBlock` Account block list

- **Example**:


::: demo


```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getOnroadBlocksByAddress",
    "params": [
        "vite_00000000000000000000000000000000000000042d7ef71894",
        0, 
        1
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
        {
            "blockType": 2,
            "hash": "6301891cee55aa123be4ac4762d2d19cf3e960b84d343b848f41dc7a2c775030",
            "prevHash": "a7c0ded4733b0b8e9d6a15c98d53020db18cc3be1005aeb288cbdae4de7aee23",
            "accountAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
            "publicKey": "P8UiTllDO/9PSMg8DrTt6g5MQuppfgTN7HF9A+UNUgA=",
            "toAddress": "vite_00000000000000000000000000000000000000042d7ef71894",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "fromBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
            "data": "/cF/JQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAnMxAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
            "logHash": null,
            "nonce": null,
            "sendBlockList": [],
            "signature": "1jS6qK9qArQGu0M850tJ05bQHoWLj/gNDVf7qzhA5AEXRoIvLloxPVAKtbzwkrb0nRXRYP3Y/X2OggIEeHPYCA==",
            "fromAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
            "height": "5318",
            "quota": "62000",
            "amount": "0",
            "fee": "0",
            "difficulty": null,
            "timestamp": 1555592008,
            "confirmedTimes": "3",
            "confirmedHash": "edf77dd2eb904c56002c87b3cb965c0d33c129cf9ef6f02adc1f08faf63d2acc",
            "tokenInfo": {
                "tokenName": "Vite Token",
                "tokenSymbol": "VITE",
                "totalSupply": "1000000000000000000000000000",
                "decimals": 18,
                "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0
            },
            "receiveBlockHeight": "",
            "receiveBlockHash": null
        }
    ]
}
```

:::

## onroad_getOnroadInfoByAddress <Badge text="public"/>

Return the information of tokens in all open transactions waiting to be received by specified account

- **Parameters**:

  *  `Address`- Account address

- **Return**:

  * ``[]Object``: 
    * `accountAddress`: `Address` Account address
    * `totalNumber`: `string` Total open transaction number
    * `tokenBalanceInfoMap`: `Map[tokenId]Object`
        * `tokenInfo`: `Object` Token information
            * `tokenName`: `string` Token name
            * `tokenSymbol`: `string` Token symbol
            * `tokenId`: `TokenId` Token Id
            * `totalSupply`: `*string` Total supply
            * `decimals`: `uint8` Decimal digits
            * `owner`: `Address` Owner's address
            * `maxSupply`: `*string` Max supply
            * `ownerBurnOnly`: `bool` Whether the token can be burned by the owner only
            * `isReIssuable`: `bool` Whether the token can be re-issued
            * `index`: `uint16` index
        * `totalAmount`: `*string` Total pending amount in this token
        * `number`: `string` Total open transaction number in this token

- **Example**:


::: demo


```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getAccountOnroadInfo",
    "params": [
        "vite_00000000000000000000000000000000000000042d7ef71894"
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "accountAddress": "vite_00000000000000000000000000000000000000042d7ef71894",
        "totalNumber": "5",
        "tokenBalanceInfoMap": {
            "tti_5649544520544f4b454e6e40": {
                "tokenInfo": {
                    "tokenName": "Vite Token",
                    "tokenSymbol": "VITE",
                    "totalSupply": "1000000000000000000000000000",
                    "decimals": 18,
                    "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0
                },
                "totalAmount": "0",
                "number": "5"
            }
        }
    }
}
```
:::

## onroad_getOnroadBlocksInBatch <Badge text="private" type="error"/>

Return all open transactions waiting to be received by a list of specified accounts

- **Parameters**:

`[]Object`: Up to 10 accounts
  * `Address`: Account address
  * `uint64`: Page index
  * `uint64`: Page size up to 256

- **Return**:

  * `map[Address][]AccountBlock`

- **Example**:


::: demo


```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getOnroadBlocksInBatch",
    "params": [
        [
    	    {
    		"addr": "vite_00000000000000000000000000000000000000042d7ef71894", 
    		"pageNum": 0 ,
    		"pageCount": 1
    	},
    	    	{
    		"addr": "vite_00000000000000000000000000000000000000042d7ef71894", 
    		"pageNum": 0 ,
    		"pageCount": 1
    	}
    	]]    
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "vite_00000000000000000000000000000000000000042d7ef71894": [
            {
                "blockType": 2,
                "hash": "3c21c7f27517c23b9749545a24c94077c8c1a01c0b4a51215bdc4ffde96de2a3",
                "prevHash": "6d0df63200792e1734ba52fdd4d1100e087d6d8c643e6a2bd050158ff558faaa",
                "accountAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
                "publicKey": "P8UiTllDO/9PSMg8DrTt6g5MQuppfgTN7HF9A+UNUgA=",
                "toAddress": "vite_00000000000000000000000000000000000000042d7ef71894",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "fromBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
                "data": "/cF/JQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAnMxAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
                "logHash": null,
                "nonce": null,
                "sendBlockList": [],
                "signature": "9rdpoB/e/VmXmwI779y3Uuz5lkXG9cO7hkOjO/gxi1Nq1Mp1JQUcaliRP9LDcFU/2CV8GMVX6VmSw3Ph7H/fDA==",
                "fromAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
                "height": "83",
                "quota": "62000",
                "amount": "0",
                "fee": "0",
                "difficulty": null,
                "timestamp": 1555578070,
                "confirmedTimes": "3",
                "confirmedHash": "ce4694f7769dc839b7dde62b179cb0d96566cc7c64cb0bd61e62f2e167a31376",
                "tokenInfo": {
                    "tokenName": "Vite Token",
                    "tokenSymbol": "VITE",
                    "totalSupply": "1000000000000000000000000000",
                    "decimals": 18,
                    "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                    "tokenId": "tti_5649544520544f4b454e6e40",
                    "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                    "ownerBurnOnly": false,
                    "isReIssuable": true,
                    "index": 0
                },
                "receiveBlockHeight": "",
                "receiveBlockHash": null
            }
        ]
    }
}
```
:::

## onroad_getOnroadInfoInBatch <Badge text="private" type="error"/>

Return the information of tokens in all open transactions waiting to be received by a list of specified accounts

- **Parameters**:
  * `[]Address`- Account addresses, up to 10

- **Return**:

  * ``[]Object``:  
    * `accountAddress`: `Address` Account address
    * `totalNumber`: `string` Total number
    * `tokenBalanceInfoMap`: `Map[tokenId]Object`
        * `tokenInfo`: `Object` Token information
            * `tokenName`: `string` Token name
            * `tokenSymbol`: `string` Token symbol
            * `tokenId`: `TokenId` Token Id
            * `totalSupply`: `*string` Total supply
            * `decimals`: `uint8` Decimal digits
            * `owner`: `Address` Owner's address
            * `maxSupply`: `*string` Max supply
            * `ownerBurnOnly`: `bool` Whether the token can be burned by the owner only
            * `isReIssuable`: `bool` Whether the token can be re-issued
            * `index`: `uint16` index
        * `totalAmount`: `*string` Total pending amount in this token
        * `number`: `string` Total open transaction number in this token

- **Example**:


::: demo


```json tab:Request
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getOnroadInfoInBatch",
    "params": [
        [
            "vite_00000000000000000000000000000000000000042d7ef71894",
            "vite_00000000000000000000000000000000000000042d7ef71894"
        ]
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
        {
            "accountAddress": "vite_00000000000000000000000000000000000000042d7ef71894",
            "totalNumber": "11",
            "tokenBalanceInfoMap": {
                "tti_5649544520544f4b454e6e40": {
                    "tokenInfo": {
                        "tokenName": "Vite Token",
                        "tokenSymbol": "VITE",
                        "totalSupply": "1000000000000000000000000000",
                        "decimals": 18,
                        "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                        "tokenId": "tti_5649544520544f4b454e6e40",
                        "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                        "ownerBurnOnly": false,
                        "isReIssuable": true,
                        "index": 0
                    },
                    "totalAmount": "0",
                    "number": "11"
                }
            }
        }
    ]
}
```
:::

## onroad_getContractOnRoadTotalNum <Badge text="private" type="error"/>

Return open transaction number waiting to be handled by specified contract

- **Parameters**:
  * `Address` Contract address
  * `Gid` Consensus group id that above contract belongs to. Optional, default value is "00000000000000000002"

- **Return**:
 * `uint64` Open transaction number

- **Example**:

::: demo

```json tab:Request 1
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getContractOnRoadFrontBlocks",
    "params": [
        "vite_0000000000000000000000000000000000000004d28108e76b"
    ]
}
```

```json tab:Request 2
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getContractOnRoadFrontBlocks",
    "params": [
        "vite_0000000000000000000000000000000000000004d28108e76b",
        "00000000000000000002"
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 3
}
```

:::

## onroad_getContractOnRoadFrontBlocks <Badge text="private" type="error"/>

Return all callers' earliest open transactions waiting to be handled by specified contract

- **Parameters**:
  * `Address` Contract address
  * `Gid` Consensus group id that above contract belongs to. Optional, default value is "00000000000000000002"

- **Return**:
  * `[]AccountBlock` All callers' earliest open transactions

- **Example**:

::: demo

```json tab:Request 1
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getContractOnRoadFrontBlocks",
    "params": [
        "vite_0000000000000000000000000000000000000004d28108e76b"
    ]
}
```

```json tab:Request 2
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "onroad_getContractOnRoadFrontBlocks",
    "params": [
        "vite_0000000000000000000000000000000000000004d28108e76b",
        "00000000000000000002"
    ]
}
```

```json tab:Response
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
        {
            "blockType": 2,
            "hash": "318d96b93f384dbdb0541b6b727accea00c7e5054d9d19bdc5bfc2b536d61741",
            "prevHash": "36e33ccadde3e19a9db8a4bc190a232d35b48ecdb64256710be508337f218f47",
            "accountAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
            "publicKey": "P8UiTllDO/9PSMg8DrTt6g5MQuppfgTN7HF9A+UNUgA=",
            "toAddress": "vite_0000000000000000000000000000000000000004d28108e76b",
            "tokenId": "tti_5649544520544f4b454e6e40",
            "fromBlockHash": "0000000000000000000000000000000000000000000000000000000000000000",
            "data": "/cF/JQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAnMxAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
            "logHash": null,
            "nonce": null,
            "sendBlockList": [],
            "signature": "EKimxy6MrBuLA5inO7EfrUpUYL+TxN3XS8VvJYbI+QOK54rsP6h/Oo8VOVDKYH5/3omKtlqsvsbfct7f9GlWAQ==",
            "fromAddress": "vite_360232b0378111b122685a15e612143dc9a89cfa7e803f4b5a",
            "height": "162",
            "quota": "62000",
            "amount": "0",
            "fee": "0",
            "difficulty": null,
            "timestamp": 1556437168,
            "confirmedTimes": "1",
            "confirmedHash": "10b46915030a4801aef731ad538eb2ca10d0d482fbd723d61e4e2f2328eab941",
            "tokenInfo": {
                "tokenName": "Vite Token",
                "tokenSymbol": "VITE",
                "totalSupply": "1000000000000000000000000000",
                "decimals": 18,
                "owner": "vite_ab24ef68b84e642c0ddca06beec81c9acb1977bbd7da27a87a",
                "tokenId": "tti_5649544520544f4b454e6e40",
                "maxSupply": "115792089237316195423570985008687907853269984665640564039457584007913129639935",
                "ownerBurnOnly": false,
                "isReIssuable": true,
                "index": 0
            },
            "receiveBlockHeight": "",
            "receiveBlockHash": null
        }
    ]
}
```

:::
