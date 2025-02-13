---
sidebarDepth: 4
title: START
---

# Start
## Description
* **IPC**：Supported in all API

    1. **\*nix(linux darwin)**: `Unix Domain Socket` file is    `~/.gvite/testdata/gvite.ipc`

    2. **Windows**: Due to` Named Pipe` naming limitation the file is  `\\.\pipe\gvite.ipc`
* **Http**：Public API ONLY. Default port is **48132**. Wallet module is excluded.

* **WebSocket**：Public API ONLY. Default port is **31420**. Wallet module is excluded.

* **Note**:
    1. To avoid unexpected behaviors, standard **JSON RPC 2.0** library is highly recommended;
    
    2. Term transaction or Tx is equivalent to account block.

:::warning
* Byte array should be converted to base64 encoding
* `uint64` and `big.int` are passed in string
:::

## Common RPC Errors

|  Description | Code | Message | Example |
|:------------:|:-----------:|:-----:|:-----:|
| Failed to parse JSON string	|  `-32700` | JSON parse failure |{"code":-32700,"message":"missing request id"}|
| Invalid JSON request	|  `-32600` | Invalid request |{"code":-32600,"message":"Unable to parse subscription request"}|
| Method not found. Please check if corresponding module has been configured in `PublicModules`	|  `-32601` | Method not found |{"code":-32601,"message":"The method tx_sendRawTx does not exist/is not available"}|
| Parameter type error |  `-32602` | Invalid parameter |{"code":-32602,"message":"missing value for required argument"}|
| Service closed |  `-32000` | Server shut down |{"code":-32000,"message":"server is shutting down"}|
| Service temporarily unavailable. Please try again later | `-32001` | Server panic |{"code":-32001,"message":"server execute panic"}|
| Callback error | `-32002` | Callback error |{"code":-32002,"message":"notifications not supported"}|

## Common Business Errors

|  Description | Code | Message | Example |
|:------------:|:-----------:|:-----:|:-----:|
| Wrong password	|  `-34001` | Key decryption error |{"code":-34001,"message":"error decrypting key"}|
| Insufficient balance |  `-35001` | Insufficient balance for transfer |{"code":-35001,"message":"insufficient balance for transfer"}|
| Insufficient quota |  `-35002` | Out of quota |{"code":-35002,"message":"out of quota"}|
| Invalid parameter |  `-35004` | Invalid method param |{"code":-35004,"message":"invalid method param"}|
| Too many PoW requests |  `-35005` | PoW called twice within one snapshot block |{"code":-35005,"message":"calc PoW twice referring to one snapshot block"}|
| ABI Method not found |  `-35006` | ABI method not found |{"code":-35006,"message":"abi: method not found"}|
| Invalid confirm time upon contract creation |  `-35007` | Invalid confirm time |{"code":-35007,"message":"invalid confirm time"}|
| Contract not found |  `-35008` | Contract not exist |{"code":-35008,"message":"contract not exists"}|
| Invalid quota ratio upon contract creation |  `-35010` | Invalid quota ratio |{"code":-35010,"message":"invalid quota ratio"}|
| Invalid block producing address |  `-36001`  |  Block producing address not valid |{"code":-36001, "message":"general account's sendBlock.Height must be larger than 1"}|
| Hash verification failure |  `-36002`  | Hash verification failed | {"code":-36002,"message":"verify hash failed"} |
| Signature verification failure |  `-36003`  | Signature verification failed | {"code":-36003,"message":"verify signature failed"} |
| Invalid PoW nonce |  `-36004`  | PoW nonce check failed | {"code":-36004,"message":"check pow nonce failed"} |
| PreHash verification failure |  `-36005`  | PreHash verification failed | {"code":-36005,"message":"verify prevBlock failed, incorrect use of prevHash or fork happened"} |
| Pending for blocks |  `-36006`  | Pending for block referred to | {"code":-36006,"message":"verify referred block failed, pending for them"} |

## JSON-RPC Support

|  JSON-RPC 2.0  | HTTP | IPC |Publish–Subscribe |WebSocket |
|:------------:|:-----------:|:-----:|:-----:|:-----:|
| &#x2713;|  &#x2713; |  &#x2713; |&#x2713;|&#x2713;|
