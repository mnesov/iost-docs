---
id: version-3.0.5-API
title: API
sidebar_label: API
original_id: API
---



## /getNodeInfo
##### GET

Returns information of the IOST server node  

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getNodeInfo
```

### Response  

A successful response may look like this:

```
200 OK

{
    "build_time": "20181208_161822+0800",
    "git_hash": "1f540ec5b619812cb01b7bbc3dd89dbd3849c6fb",
    "mode": "ModeNormal",
    "network": {
        "id": "12D3KooWGGauAVW7vQw33kAAttbyTVf81Urpi2f4LYBAXTYzhwqj",
        "peer_count": 1,
        "peer_info": [{
            "id": "12D3KooWPSPLPyDFtcbKUvQGWM7pCXWEhRAjA1A5nAAFEvnce1Dm",
            "addr": "/ip4/127.0.0.1/tcp/50004"
        }]
    }
}
```

Key             |Type       |Description 
----                |--         |--
build\_time |string         |Building time of the 'server' binary
git\_hash       |string     |Git hash of the 'iserver' binary
mode            |string     |Current mode of the server. It can be one of 'ModeInit', 'ModeNormal' and 'ModeSync'
network     |[NetworkInfo](#network)|Network information of the node 

### NetworkInfo

Key             |Type       |Description 
----                |--         |--
id                  |string         |Node ID in the p2p network
peer\_count |int32      |Peer count of the node
peer\_info      |[PeerInfo]|Peer information of the node

### PeerInfo

Key             |Type       |Description 
----                |--         |--
id                  |string     |ID of the peer
addr                |struct     |Address of the idx-th peer




## /getChainInfo
##### GET

Returns information of the IOST blockchain  

### Request 

A request may look like this:

```
curl http://127.0.0.1:30001/getChainInfo
```

### Response

A successful response looks like this:

```
200 OK

{
    "net_name": "debugnet",
    "protocol_version": "1.0",
    "chain_id": 1024,
    "head_block": "16041",
    "head_block_hash": "DLJVtko6nQnAdvQ7y6dXHo3WMdG324yRLz8tPKk9tGHu",
    "lib_block": "16028",
    "lib_block_hash": "8apn7vCvQ6s9PFBzGfaXrvyL5eAaLNc4mEAgnTMoW8tC",
    "witness_list": ["IOST2K9GKzVazBRLPTkZSCMcyMayKv7dWgdHD8uuWPzjfPdzj93x6J", "IOST2YKPmRDGy5xLR7Gv65CN5nQ3vMmVhRjAsEM7Gj9xcB1LWgZUAd", "IOST7E4T5rG9wjPZXDeM1zjhhWU3ZswtPQ1heeRUFUxntr65sYRBi"],
    "lib_witness_list": ["IOST2K9GKzVazBRLPTkZSCMcyMayKv7dWgdHD8uuWPzjfPdzj93x6J", "IOST2YKPmRDGy5xLR7Gv65CN5nQ3vMmVhRjAsEM7Gj9xcB1LWgZUAd", "IOST7E4T5rG9wjPZXDeM1zjhhWU3ZswtPQ1heeRUFUxntr65sYRBi"],
	"pending_witness_list": ["IOST2K9GKzVazBRLPTkZSCMcyMayKv7dWgdHD8uuWPzjfPdzj93x6J", "IOST2YKPmRDGy5xLR7Gv65CN5nQ3vMmVhRjAsEM7Gj9xcB1LWgZUAd", "IOST7E4T5rG9wjPZXDeM1zjhhWU3ZswtPQ1heeRUFUxntr65sYRBi"],
	"head_block_time": "1552917911507043000",
	"lib_block_time": "1552917911507043000"
}
```

Key                     |Type       |Description 
----                        |--         |--
net\_name           |string     |Network name, such as "mainnet" or "testnet"
protocol\_version   |string     |iost protocol version
chain\_id   | uint32     |iost chain id
head\_block         |int64      |the lastest block height
head\_block\_hash|string        |the hash of the lastest block
lib\_block              |int64      |height of irreversible blocks
lib\_block\_hash    |int64      |hash of irreversible blocks
witness\_list           |repeated string|list of pubkeys for the current block production nodes
lib\_witness\_list |repeated string  | list of pubkeys for the block production nodes of the last irreversible block time
pending\_witness\_list |repeated string  | list of pubkeys for the next round block production nodes 
head_block_time |int64  | time of head block
lib_block_time |int64  | time of last irreversible block

## /getGasRatio
##### GET

Get the GAS multiplier information, so that users may set their desired GAS trading multipliers. We recommend a slightly higher gas ratio than lowest_gas_ratio so that transactions will be published timely.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getGasRatio
```

### Response

A successful response may look like this:

```
200 OK

{
    "lowest_gas_ratio": 1.5,
    "median_gas_ratio": 1.76
}
```

Key                 |Type       |Description 
----                    |--         |--
lowest\_gas\_ratio|double|the lowest gas ratio of the most recently packed blocks
median\_gas\_ratio|double|the median gas ratio of the most recently packed blocks


## /getRAMInfo
##### GET

Get RAM information for the current blockchain, including usage and price.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getRAMInfo
```

### Response

A successful response may look like this:

```
200 OK

{
    "available_ram": "96207067431",
    "buy_price": 0.04227129323234719,
    "sell_price": 0.00014551844642842057,
    "total_ram": "137438953472",
    "used_ram": "41231886041"
}
```

Key                 |Type       |Description 
----                    |--         |--
available\_ram  |int64      |RAM available, in byte
used\_ram       |int64      |The amount of RAM sold, in byte
total\_ram          |int64      |The system's total RAM count, in byte
buy\_price      |double |The buying price of RAM, in IOST/byte
sell\_price         |double |The selling price of RAM, in IOST/byte






## /getTxByHash
##### GET

Fetches the transaction by its base58 encoded hash  

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getTxByHash/6eGkZoXPQtYXdh7dBSXe2L1ckUCDj4egRn4fXtS2ACnR
```

Key                 |Type       |Description 
----                    |--         |--
hash                |string     |hash of the transaction

### Response

A successful response may look like this:

```
200 OK

{
    "status": "IRREVERSIBLE",
    "transaction": {
        "hash": "6eGkZoXPQtYXdh7dBSXe2L1ckUCDj4egRn4fXtS2ACnR",
        "time": "1544269519362042000",
        "expiration": "1544279519362041000",
        "gas_ratio": 1,
        "gas_limit": 50000,
        "delay": "0",
        "chain_id": 1024,
        "actions": [{
            "contract": "ContractTBv8ZDKUhTyeS4MomdcHRrXnJMELa5usSMHP6QJntFQ",
            "action_name": "transfer",
            "data": "[\"admin\",\"i1544269477\",1]"
        }],
        "signers": [],
        "publisher": "admin",
        "referred_tx": "",
        "amount_limit": [],
        "tx_receipt": null
    },
    "block_number": "4047298"
}
```

Key                 |Type       |Description 
----                    |--         |--
status              |enum       |PENDING- transaction is cached, PACKED - transaction is in reversible blocks, IRREVERSIBLE - transaction is in irreversible blocks
transaction     |Transaction|Transaction data
block_number | string   | the number of the block which the tx is in

### Transaction

Key                 |Type       |Description 
----                    |--         |--
hash                |string     |transaction's hash
time                    |int64      |timestamp of the transaction
expiration      |int64      |the expiration of the transaction
gas_ratio           |double |GAS ratio, we recommend it to be 1.00 (1.00 – 100.00). Raise the ratio to let the network pack it faster
gas_limit           |double |Upper limits of GAS. This transaction will never cost more GAS than this amount
delay               |int64      |Transactions will be delayed by this much, in nanosecond
chain_id               |uint32      | id of blockchain on which the transaction could be executed
actions         |repeated Action|the smallest transaction execution unit
signers         |repeated string|list of transaction signatures
publisher           |string     |sender of the transaction, who is responsible for fees
referred_tx     |string     |dependency of transaction generation; used for delayed transactions
amount_limit    |repeated AmountLimit|Users may specify token limits. For example, {"iost": 100} specifies each signers will not spend more than 100 IOST for the transaction
tx_receipt      |TxReceipt|the receipt of the transaction Action

### Action

Key                 |Type       |Description 
----                    |--         |--
contract            |string     |contract name
action_name |string     |function name of the contract
data                    |string     |Specific parameters of the call. Put every parameter in an array, and JSON-serialize this array. It may looks like `["a_string", 13]`

### AmountLimit

Key                 |Type       |Description 
----                    |--         |--
token               |string     |token name
value               |double |corresponding token limit

### TxReceipt

Key                 |Type       |Description 
----                    |--         |--
tx_hash         |string     |hash of the transaction
gas_usage       |double |GAS consumption of the transaction
ram_usage       |map\<string, int64\>|RAM consumption for the transaction. map-key is account name, and value is RAM amount
status_code |enum       |Status of the transaction. SUCCESS; GAS_RUN_OUT - insufficient GAS; BALANCE_NOT_ENOUGH - insufficient balance; WRONG_PARAMETER; RUNTIME_ERROR - a run-time error; TIMEOUT; WRONG_TX_FORMAT; DUPLICCATE_SET_CODE - set code is duplicated unexpectedly; UNKNOWN_ERROR
message         |string     |a message descripting status_code
returns         |repeated string    |return values for each Action
receipts            |repeated Receipt|for event functions

### Receipt

Key                 |Type       |Description 
----                    |--         |--
func_name       |string     |ABI function name
content         |string     |content

<!-- CONTINUE HERE: http://developers.iost.io/docs/zh-CN/next/6-reference/API/#gettxreceiptbytxhash-hash -->


## /getTxReceiptByTxHash/{hash}
##### GET

Get transaction receipt data with transaction hash.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getTxReceiptByTxHash/6eGkZoXPQtYXdh7dBSXe2L1ckUCDj4egRn4fXtS2ACnR
```

Key                 |Type       |Description 
----                    |--         |--
hash                |string     |hash of the receipt

### Response

A successful response may look like this:

```
200 OK

{
    "tx_hash": "6eGkZoXPQtYXdh7dBSXe2L1ckUCDj4egRn4fXtS2ACnR",
    "gas_usage": 6633,
    "ram_usage": {
        "admin": "0",
        "issue.iost": "0"
    },
    "status_code": "SUCCESS",
    "message": "",
    "returns": ["[\"\"]"],
    "receipts": [{
        "func_name": "token.iost/transfer",
        "content": "[\"iost\",\"admin\",\"i1544269477\",\"1\",\"\"]"
    }]
}
```

Key                 |Type       |Description 
----                    |--         |--
                        |TxReceipt|receipt of the transaction




## /getBlockByHash/{hash}/{complete}
##### GET

Get block information with block hash.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getBlockByHash/4c9GHyGLi6hUqB4d6zGFcywycYKucsmWsbgvhPe31GaY/false
```

Key                 |Type       |Description 
----                    |--         |--
hash                |string     |block hash
complete            |bool       |true - show detailed transactions within the block; false - don't.

### Response

A successful response may look like this:

```
200 OK

{
    "status": "IRREVERSIBLE",
    "block": {
        "hash": "4c9GHyGLi6hUqB4d6zGFcywycYKucsmWsbgvhPe31GaY",
        "version": "0",
        "parent_hash": "G4njPLnYskU4DcuTz5CwpLPETcfH6yN78V8emge8t21f",
        "tx_merkle_hash": "HHKAG2D7Kon2on5SqV66ZsfdNk9Wus8yhWqdTb86wgPJ",
        "tx_receipt_merkle_hash": "FXr8Mf7hr568MP23BFWJiBUej2xSj3M7416WAKJpswzx",
        "number": "2",
        "witness": "IOST2YKPmRDGy5xLR7Gv65CN5nQ3vMmVhRjAsEM7Gj9xcB1LWgZUAd",
        "time": "1544262978309033000",
        "gas_usage": 0,
        "tx_count": "1",
        "info": null,
        "transactions": []
    }
}
```

Key                 |Type       |Description 
----                    |--         |--
status              |enum       |PENDING - block is in cache; IRREVERSIBLE - block is irreversible.
block               |Block      |a Block struct

### Block

Key                 |Type       |Description 
----                    |--         |--
hash                |string     |block hash
version         |int64      |block version number
parent\_hash    |string     |the hash of the parent block of this block
tx\_merkle\_hash    |string |the merkle tree hash of all transactions
tx\_receipt\_merkle\_hash   |string |the merkle tree hash of all receipts
number          |int64      |block number
witness         |string     |public key of the block producer
time                    |int64      |time of block production
gas\_usage      |double |total GAS consumption within the block
tx\_count           |int64      |transaction number in the block
info           | Info      |(This key is reserved.)
transactions    |repeated Transaction   |all the transactions.

### Info

Key                 |Type       |Description 
----                    |--         |--
mode                |int32      |mode of concurrency; 0 - non-concurrent; 1 - concurrent
thread              |int32      |the thread count of transaction concurrent execution
batch_index |repeated int32 |indices of the transaction


## /getBlockByNumber/{number}/{complete}
##### GET

Get block information using the block number.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getBlockByNumber/3/false
```

Key                 |Type       |Description 
----                    |--         |--
number          |int64      |block number
complete            |bool       |true - display transactions of the block; false - don't.


### Response

A successful response may look like this:

```
200 OK

{
    "status": "IRREVERSIBLE",
    "block": {
        "hash": "HPZyoPQ44vsyLDRspjgrySyHnpuiGwckPx8uNtHZugJW",
        "version": "0",
        "parent_hash": "4c9GHyGLi6hUqB4d6zGFcywycYKucsmWsbgvhPe31GaY",
        "tx_merkle_hash": "HHKAG2D7Kon2on5SqV66ZsfdNk9Wus8yhWqdTb86wgPJ",
        "tx_receipt_merkle_hash": "62pESNUGDVsH4B1BCymJvmjGxPu5bb4R3u4x45K9Ybdq",
        "number": "3",
        "witness": "IOST2YKPmRDGy5xLR7Gv65CN5nQ3vMmVhRjAsEM7Gj9xcB1LWgZUAd",
        "time": "1544262978609003000",
        "gas_usage": 0,
        "tx_count": "1",
        "info": null,
        "transactions": []
    }
}
```

Key                 |Type       |Description 
----                    |--         |--
status              |enum       |PENDING - block is in cache; IRREVERSIBLE - block is not reversible
block               |Block      |the block struct







## /getAccount/{name}/{by_longest_chain}
##### GET

Get account information.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getAccount/admin/true
```

Key                 |Type       |Description 
----                    |--         |--
name                |string     |the account name
by\_longest\_chain  |bool   |true - get data from the longest chain; false - get data from irreversible blocks


### Response

A successful response may look like this:

```
200 OK

{
    "name": "admin",
    "balance": 982678652,
    "gas_info": {
        "current_total": 53102598634,
        "transferable_gas": 60000,
        "pledge_gas": 53102538634,
        "increase_speed": 330011,
        "limit": 90003000000,
        "pledged_info": [{
            "pledger": "admin",
            "amount": 3000100
        }]
    },
    "ram_info": {
        "available": "99000"
    },
    "permissions": {
        "active": {
            "name": "active",
            "group_names": [],
            "items": [{
                "id": "IOST2mCzj85xkSvMf1eoGtrexQcwE6gK8z5xr6Kc48DwxXPCqQJva4",
                "is_key_pair": true,
                "weight": "1",
                "permission": ""
            }],
            "threshold": "1"
        },
        "owner": {
            "name": "owner",
            "group_names": [],
            "items": [{
                "id": "IOST2mCzj85xkSvMf1eoGtrexQcwE6gK8z5xr6Kc48DwxXPCqQJva4",
                "is_key_pair": true,
                "weight": "1",
                "permission": ""
            }],
            "threshold": "1"
        }
    },
    "groups": {},
    "frozen_balances": [],
    "vote_infos": []
}
```

Key                 |Type       |Description 
----                    |--         |--
name                |string     |account name
balance         |double |the balance of the account
gas\_info           |GasInfo    |Gas information
ram\_info           |RAMInfo    |Ram information
permissions |map<string, Permission>    |permissions
groups              |map<string, Group>         |permission groups
frozen\_balances    |repeated FrozenBalance |information on the frozen balance
vote\_infos    |repeated VoteInfo |information of vote

### GasInfo

Key                 |Type       |Description 
----                    |--         |--
current\_total  |double |Total gas for the moment
transferable\_gas   |double |Gas available for trade
pledge\_gas     |double |Gas obtained from deposits
increase\_speed |double |The rate of gas increase, in gas per second
limit                   |double |The upper limit of gas from token deposit
pledged\_info   |repeated PledgeInfo    |The information on deposit made by other accounts, on behalf of the inquired account

### PledgeInfo

Key                 |Type       |Description 
----                    |--         |--
pledger         |string     |the account receiving the deposit
amount          |double |the amount of the deposit

### RAMInfo

Key                 |Type       |Description 
----                    |--         |--
available           |int64      |RAM bytes available for use
used           |int64      |RAM bytes used
total           |int64      |RAM bytes total

### Permission

Key                 |Type       |Description 
----                    |--         |--
name                |string     |permission name
group_names              |repeated string    |permission group names
items               |repeated Item  |permission information
threshold           |int64      |permission threshold

### Item

Key                 |Type       |Description 
----                    |--         |--
id                      |string     |permission name or key paid ID
is_key_pair     |bool       |true - id is a key pair; false - id is a permission name
weight              |int64      |permission weight
permission      |string     |the permission

### Group

Key                 |Type       |Description 
----                    |--         |--
name                |string     |name of the group
items               |repeated Item  |information on the permission group

### FrozenBalance

Key                 |Type       |Description 
----                    |--         |--
amount          |double |the amount
time                    |int64      |the time when the amount is unfrozen

### VoteInfo

Key                 |Type       |Description 
----                    |--         |--
option          |string |candidate
votes                    |string      |number of votes
cleared_votes                    |string      |number of votes cleared



## /getTokenBalance/{account}/{token}/{by_longest_chain}
##### GET

Get account balance of a specified token.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getTokenBalance/admin/iost/true
```

Key                 |Type       |Description 
----                    |--         |--
account         |string     |account name
token               |string     |token name
by\_longest\_chain  |bool   |true - get information from the longest chain; false - get data from irreversible blocks

### Response

A successful response may look like this:

```
200 OK

{
    "balance": 982678652,
    "frozen_balances": []
}
```

Key                 |Type       |Description 
----                    |--         |--
balance             |double |the balance
frozen\_balances    |repeated FrozenBalance |the information on frozen balance


## /GetProducerVoteInfo/{name}/{by_longest_chain}
##### GET

Get producer vote infomation

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getProducerVoteInfo/producerName/true
```

Key                 |Type       |Description 
----                    |--         |--
id                      |string     |producer Name
by\_longest\_chain  |bool   |true - get data from longest chain; false - get data from irreversible blocks

### Response

A successful response may look like this:

```
{
    pubkey: "9V1v7Emef8MyPc1uBc9i5BmrTFxpUkxvQa1vUUSuzr4F",
    loc: "",
    url: "",
    net_id: "12D3KooWMQnia3aw9Yp7yrbeMB8KhTWYxaSdbNf6FBketXJs4n76",
    is_producer: true,
    status: "APPROVED",
    online: true,
    votes: 2100000,
}
```


## /getContract/{id}/{by_longest_chain}
##### GET

Get contract information using contract ID.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getContract/base.iost/true
```

Key                 |Type       |Description 
----                    |--         |--
id                      |string     |contract ID
by\_longest\_chain  |bool   |true - get data from longest chain; false - get data from irreversible blocks


### Response

A successful response may look like this:

```
200 OK

{
    "id": "base.iost",
    "code": "const producerPermission = 'active';\nconst voteStatInterval = 200;\nclass Base {\n    constructor() {\n    }\n    init() {\n        _IOSTInstruction_counter.incr(12);this._put('execBlockNumber', 0);\n    }\n    InitAdmin(adminID) {\n        _IOSTInstruction_counter.incr(4);const bn = block.number;\n        if (_IOSTInstruction_counter.incr(8),_IOSTBinaryOp(bn, 0, '!==')) {\n            _IOSTInstruction_counter.incr(14);throw new Error('init out of genesis block');\n        }\n        _IOSTInstruction_counter.incr(12);this._put('adminID', adminID);\n    }\n    can_update(data) {\n        _IOSTInstruction_counter.incr(12);const admin = this._get('adminID');\n        _IOSTInstruction_counter.incr(12);this._requireAuth(admin, producerPermission);\n        return true;\n    }\n    _requireAuth(account, permission) {\n        _IOSTInstruction_counter.incr(12);const ret = BlockChain.requireAuth(account, permission);\n        if (_IOSTInstruction_counter.incr(8),_IOSTBinaryOp(ret, true, '!==')) {\n            _IOSTInstruction_counter.incr(22);throw new Error(_IOSTBinaryOp('require auth failed. ret = ', ret, '+'));\n        }\n    }\n    _get(k) {\n        _IOSTInstruction_counter.incr(12);const val = storage.get(k);\n        if (_IOSTInstruction_counter.incr(8),_IOSTBinaryOp(val, '', '===')) {\n            return null;\n        }\n        _IOSTInstruction_counter.incr(12);return JSON.parse(val);\n    }\n    _put(k, v) {\n        _IOSTInstruction_counter.incr(24);storage.put(k, JSON.stringify(v));\n    }\n    _vote() {\n        _IOSTInstruction_counter.incr(12);BlockChain.callWithAuth('vote_producer.iost', 'Stat', `[]`);\n    }\n    _bonus(data) {\n        _IOSTInstruction_counter.incr(24);BlockChain.callWithAuth('bonus.iost', 'IssueContribute', JSON.stringify([data]));\n    }\n    _saveBlockInfo() {\n        _IOSTInstruction_counter.incr(12);let json = storage.get('current_block_info');\n        _IOSTInstruction_counter.incr(36);storage.put(_IOSTBinaryOp('chain_info_', block.parentHash, '+'), JSON.stringify(json));\n        _IOSTInstruction_counter.incr(24);storage.put('current_block_info', JSON.stringify(block));\n    }\n    Exec(data) {\n        _IOSTInstruction_counter.incr(12);this._saveBlockInfo();\n        _IOSTInstruction_counter.incr(4);const bn = block.number;\n        _IOSTInstruction_counter.incr(12);const execBlockNumber = this._get('execBlockNumber');\n        if (_IOSTInstruction_counter.incr(8),_IOSTBinaryOp(bn, execBlockNumber, '===')) {\n            return true;\n        }\n        _IOSTInstruction_counter.incr(12);this._put('execBlockNumber', bn);\n        if (_IOSTInstruction_counter.incr(16),_IOSTBinaryOp(_IOSTBinaryOp(bn, voteStatInterval, '%'), 0, '===')) {\n            _IOSTInstruction_counter.incr(12);this._vote();\n        }\n        _IOSTInstruction_counter.incr(12);this._bonus(data);\n    }\n}\n_IOSTInstruction_counter.incr(7);module.exports = Base;",
    "language": "javascript",
    "version": "1.0.0",
    "abis": [{
        "name": "Exec",
        "args": ["json"],
        "amount_limit": []
    }, {
        "name": "can_update",
        "args": ["string"],
        "amount_limit": []
    }, {
        "name": "InitAdmin",
        "args": ["string"],
        "amount_limit": []
    }, {
        "name": "init",
        "args": [],
        "amount_limit": []
    }]
}
```

Key                 |Type       |Description 
----                    |--         |--
id                      |string     |contract ID
code                |string     |the code of the contract
language            |string     |the language of the contract
version         |string     |contract version
abis                    |repeated ABI   |the ABIs of the contract

### ABI

Key                 |Type       |Description 
----                    |--         |--
name                |string     |interface name
args                    |repeated string    |arguments of the interface
amount\_limit   |repeated AmountLimit   |The limits on the amount





## /getContractStorage
##### POST

Get contract storage data locally.

### Request

A request may look like this:

```
curl -X POST http://127.0.0.1:30001/getContractStorage -d '{"id":"vote_producer.iost","field":"producer00001","key":"producerTable","by_longest_chain":true}'
```

Key                 |Type       |Description 
----                    |--         |--
id                      |string     |ID of the smart contract
field                   |string     |the values from StateDB; if StateDB\[key\] is a map then it is required to configure field to obtain values of StateDB\[key\]\[field\]
key                 |string     |the key of StateDB
by\_longest\_chain  |bool   |true - get data from the longest chain; false - get data from irreversible blocks

### Response

A successful response may look like this:

```
200 OK
{"data":"
    {
        "pubkey": "IOST2K9GKzVazBRLPTkZSCMcyMayKv7dWgdHD8uuWPzjfPdzj93x6J",
        "loc": "",
        "url": "",
        "netId": "",
        "online": true,
        "registerFee": "200000000"
    }
"}
```

## /getContractStorageFields
##### POST

Get contract storage key list of map, up to 256 are returned

### Request

A request may look like this:

```
curl -X POST http://127.0.0.1:30001/getContractStorageFields -d '{"id":"token.iost","key":"TIiost","by_longest_chain":true}'
```

Key                 |Type       |Description 
----                    |--         |--
id                      |string     |ID of the smart contract
key                 |string     |the key of StateDB
by\_longest\_chain  |bool   |true - get data from the longest chain; false - get data from irreversible blocks

### Response

A successful response may look like this:

```
200 OK
{
	"fields": ["issuer","totalSupply","supply","canTransfer","onlyIssuerCanTransfer","defaultRate","decimal","fullName"]
}
```


## /sendTx
##### POST

Publish the transaction to the node. When the node receives the transaction, it will do a sanity check and return errors if the check fails. If the check passes, the transaction will be added to the transaction pool and return a Hash of the transaction.

Users may use the hash as an argument of the `getTxByHash` API or the `getTxReceiptByTxHash` API, to look up the transaction state, and check whether execution succeeds.

**Notes:**

This API requires transaction hash and signature, and is tricky to be called directly.

<!-- 可能需要更新以下链接 -->

We recommend users send transactions with our [CLI tools](4-running-iost-node/iWallet.md).

Developers may send transactions with [JavaScript SDK](https://github.com/iost-official/iost.js).

### Request Parameters

Key                 |Type       |Description 
----                    |--         |--
time                    |int64      |Time of the transaction generation, in nanoseconds, from UnixEpoch-zero.
expiration      |int64      |The time when the transaction expires, in nanoseconds since UnixEpoch-zero. If a block-producing node receives the transaction after expiration, it will not execute the transaction.
gas\_ratio          |double |GAS ratio. This transaction will be executed with default ratio, multiplied by this parameter. The higher the ratio, the faster the transaction gets executed. The value can be reasonably between 1.0 to 100.0
gas\_limit          |double |Maximum GAS allowed by this transaction. Should not be lower than 50,000
delay               |int64      |The nanoseconds of the transaction delay. Set to 0 for non-delayed transactions.
chain_id               |uint32      |chain_id
actions         |repeated Action    |Specific calls of the transaction
amount\_limit   |repeated AmountLimit   |Limits on token of the transaction. More than one token limits may be specified; if the transaction exceeds theses limits, execution will halt.
publisher           |string     |ID of the transaction publisher
publisher\_sigs |repeated Signature |Signatures of the publisher, [as described here](/MISSING_URL_HERE.md). The publisher may provide multiple signatures for different permissions. Refer to documentations on the permission system.
signers         |repeated string    |The IDs of signers other than the publisher. May be left empty.
signatures      |repeated Signature |Signatures of the signers. Each signers should have one or many signatures, so the length of the signatures should not be less than that of the signers.

<!-- 上表中需要提供 URL -->

### Signature

Key                 |Type       |Description 
----                    |--         |--
algorithm                |string     | "ED25519" or "SECP256K1"
signature                    | string    |transaction's signature
public\_key   |string   |The public key corresponding to the signature




### Response

Key                 |Type       |Description 
----                    |--         |--
hash                |string     |the transaction hash
|pre_tx_receipt | [TxReceipt](#txreceipt)  | receipt of transaction executed in advance by RPC node, returned only when RPC node opens the switch|



### Signing a transaction

There are three steps to sign a transaction: convert the transaction struct to byte array, calculate sha3 hash of the byte array, and sign this hash with your private key.

* **Convert transaction struct to byte array**

    The algorithm is: convert each field of transaction into byte array in declarative order, and then add length before indefinite type (such as string and structure) and splice. The way the various field types are converted to byte arrays is shown in the table below.
    
    Type    |Conversion Method                          |Example
    ---     |--------------                                 |--------------------
    int     |Convert to byte array with Big-endian  |int64(1023) is converted to \[0 0 0 0 0 0 3 255\]
    string  |Splice the byte of each character in the string and add length before it    |"iost" is converted to \[0 0 0 4 105 111 115 116\]
    array   | convert each element of the array into a byte array, add length before each array, put them together   |\["iost" "iost"\] is converted to \[0 0 0 2 0 0 0 4 105 111 115 116 0 0 0 4 105 111 115 116\]
    map     |Each pair of keys: values in the dictionary is converted into byte arrays and spliced, then each pair is spliced in ascending order of keys, and the length of map is added to the front of each pair.    |\["b":"iost", "a":"iost"\] converts to \[0 0 0 2 0 0 0 1 97 0 0 0 4 105 111 115 116 0 0 0 1 98 0 0 0 4 105 111 115 116\] "

    The transaction parameters are declared in this order: "time", "expiration", "gas\_ratio", "gas\_limit", "delay", "chain_id", "reserved", "signers", "actions", "amount\_limit", and "signatures", so the pseudo-code converting a transaction struct to byte array is:   

	```
	func TxToBytes(t transaction) []byte {
			return Int64ToBytes(t.time) + Int64ToBytes(t. expiration) + 
			 		Int64ToBytes(int64(t.gas_ratio * 100)) + Int64ToBytes(int64(t.gas_limit * 100)) +     // Node that gas_ratio and gas_limit need to be multiplied by 100 and convert to int64
		 			Int64ToBytes(t.delay) + Int32ToBytes(t.chain_id) + 
		 			BytesToBytes(t.reserved) + // reserved is a reserved field. It only needs to write an empty byte array when serialized. Don't send this field in RPC request parameters.
		 			ArrayToBytes(t.signers) + ArrayToBytes(t.actions)  +
		 			ArrayToBytes(t.amount_limit) + ArrayToBytes(t.signatures)
		}
	```
    
	Refer to [go-iost](https://github.com/iost-official/go-iost/blob/master/iwallet/sdk.go#L668) for golang implementation; refer to [iost.js](https://github.com/iost-official/iost.js/blob/master/lib/structs.js#L73) for JavaScript implementation.
    
* **Calculate the hash of the byte array with sha3 algorithm**
    
    Use the sha3 libraries in your language to calculate hash of the byte array you obtained from the previous step.
    
* **Sign the hash with private key**
    
    IOST supports two asymmetric encryption algorithms: Ed25519 and Secp256k1. These two algorithms share the same signing process: generate a public-private key pair, and sign the hash from the previous step.
    
    The private key of the "publisher\_sigs" must agree with the transaction's "publisher" account. The "signatures" private keys must agrees with the transaction's "signers" accounts. "signatures" is used for multi-layer signing, and is not required; "publisher\_sigs" is required. Fees for transaction execution will be taken out from the publisher's account.
    
### Request example

Assume account "testaccount" has a transaction that transfers 100 iost to the account named "anothertest".

* **Construct the transaction**

    ```
    {
		"time": 1544709662543340000,
		"expiration": 1544709692318715000,
		"gas_ratio": 1,
		"gas_limit": 500000,
		"delay": 0,
		"chain_id": 1024,
		"signers": [],
		"actions": [
			{
				"contract": "token.iost",
				"action_name": "transfer",
				"data": "[\"iost\", \"testaccount\", \"anothertest\", \"100\", \"this is an example transfer\"]",
			},
		],
		"amount_limit": [
			{
				"token": "*",
				"value": "unlimited",
			},
		],
		"signatures": [],
	}
    ```
    
* **Calculate hash**

    After serializing and hashing the transaction, we obtain the hash "/gB8TJQibGI7Kem1v4vJPcJ7vHP48GuShYfd/7NhZ3w=".
    
* **Calculate signature**

    Assume "testaccount" has a public key with ED25519 algorithm, the public key is "lDS+SdM+aiVHbDyXapvrsgyKxFg9mJuHWPZb/INBRWY=", and the private key is "gkpobuI3gbFGstgfdymLBQAGR67ulguDzNmLXEJSWaGUNL5J0z5qJUdsPJdqm+uyDIrEWD2Ym4dY9lv8g0FFZg==". Sign the hash with the private key and we get "/K1HM0OEbfJ4+D3BmalpLmb03WS7BeCz4nVHBNbDrx3/A31aN2RJNxyEKhv+VSoWctfevDNRnL1kadRVxSt8CA=="

* **Publish transaction**

    The complete transaction parameter is:
    
    ```
    {
		"time": 1544709662543340000,
		"expiration": 1544709692318715000,
		"gas_ratio": 1,
		"gas_limit": 500000,
		"delay": 0,
		"chain_id": 1024,
		"signers": [],
		"actions": [
			{
				"contract": "token.iost",
				"action_name": "transfer",
				"data": "[\"iost\", \"testaccount\", \"anothertest\", \"100\", \"this is an example transfer\"]",
			},
		],
		"amount_limit": [
			{
				"token": "*",
				"value": "unlimited",
			},
		],
		"signatures": [],
		"publisher": "testaccount",
		"publisher_sigs": [
			{
				"algorithm": "ED25519",
				"public_key": "lDS+SdM+aiVHbDyXapvrsgyKxFg9mJuHWPZb/INBRWY=",
				"signature": "/K1HM0OEbfJ4+D3BmalpLmb03WS7BeCz4nVHBNbDrx3/A31aN2RJNxyEKhv+VSoWctfevDNRnL1kadRVxSt8CA==",
			},
		],
	}
    ```
    
    After we JSON-serialize the struct, we can send the following RPC:
    
    ```
  	curl -X POST http://127.0.0.1:30001/sendTx -d '{"actions":[{"action_name":"transfer","contract":"token.iost","data":"[\"iost\", \"testaccount\", \"anothertest\", \"100\", \"this is an example transfer\"]"}],"amount_limit":[{"token":"*","value":"unlimited"}],"delay":0,"chain_id":1024, "expiration": 1544709692318715000,"gas_limit":500000,"gas_ratio":1,"publisher":"testaccount","publisher_sigs":[{"algorithm":"ED25519","public_key":"lDS+SdM+aiVHbDyXapvrsgyKxFg9mJuHWPZb/INBRWY=","signature":"/K1HM0OEbfJ4+D3BmalpLmb03WS7BeCz4nVHBNbDrx3/A31aN2RJNxyEKhv+VSoWctfevDNRnL1kadRVxSt8CA=="}],"signatures":[],"signers":[],"time": 1544709662543340000}'
    ```


## /execTx
##### POST

Send the transaction to the node, and execute immediately. This will not seek consensus on the chain, nor will this transaction persist.

This API is used to check whether a testing contract executes as expected. Obviously, execTx cannot guarantee the same behaviour with an on-chain execution due to different time to call.

### Request

This API shares the same set of paramters with /sendTx.

### Response

This API shares the same response format with /getTxReceiptByTxHash.

## /subscribe
##### **POST**
Subscription events, including events triggered in smart contracts and transactions completed.

### Request

A request may look like this:

```
curl -X POST http://127.0.0.1:30001/subscribe -d '{"topics":["CONTRACT_RECEIPT"], "filter":{"contract_id":"token.iost"}}'
```
| Key | Type | Description |
| :----: | :-----: | :------ |
| topics |repeated enum  | topics，the enum is CONTRACT\_EVENT or CONTRACT\_RECEIPT|
| filter | [Filter](#filter)  | Received events are filtered according to the fields in the filter. If this field is not passed, event data in all topics will be received. |
### Filter
| Key | Type | Description |
| :----: | :-----: | :------ |
| contract_id | string | contract id|



### Response

A successful response may look like this:

```
{"result":{"event":{"topic":"CONTRACT_RECEIPT","data":"[\"contribute\",\"producer00001\",\"900\"]","time":"1545646637413936000"}}}
{"result":{"event":{"topic":"CONTRACT_RECEIPT","data":"[\"contribute\",\"producer00001\",\"900\"]","time":"1545646637711757000"}}}
{"result":{"event":{"topic":"CONTRACT_RECEIPT","data":"[\"contribute\",\"producer00001\",\"900\"]","time":"1545646638013188000"}}}
{"result":{"event":{"topic":"CONTRACT_RECEIPT","data":"[\"contribute\",\"producer00001\",\"900\"]","time":"1545646638317840000"}}}
...
```
| Key | Type | Description |
| :----: | :--------: | :------ |
| topic | enum  | topic，the enum is CONTRACT\_EVENT or CONTRACT\_RECEIPT|
| data | string  |event data|
| time | int64  | event timestamp|


## /getCandidateBonus/{name}/{by\_longest\_chain}
---

##### **GET**
**概要:** Query the voting bonus a node can receive.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getCandidateBonus/erebus/1
```
| Key | Type | Description |
| :----: | :-----: | :------: |
| name | string  | node account name|
| by\_longest\_chain | bool  | true - get data from the longest chain; false - get data from irreversible blocks|

### Response

A successful response may look like this:

```
200 OK
{
	"bonus": 111866.61819617
}
```

| Key | Type | Description |
| :----: | :--------: | :------ |
| bonus |double   | the bonus he can receive |


## /getVoterBonus/{name}/{by\_longest\_chain}
---

##### **GET**
**概要:** Query the voting bonus a voter can receive.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getVoterBonus/admin/1
```
| Key | Type | Description |
| :----: | :-----: | :------: |
| name | string  | voter account name|
| by\_longest\_chain | bool  | true - get data from the longest chain; false - get data from irreversible blocks|

### Response

A successful response may look like this:

```
200 OK
{
	"bonus": 94875.58356478,
	"detail":
	{
		"dapppub": 15414.37339835,
		"iostamerica": 17212.96477434,
		"laomao": 9895.73931972,
		"metanyx": 29877.55014659,
		"sutler": 20924.99488913,
		"tokenpocket": 1549.96103665
	}
}
```

| Key | Type | Description |
| :----: | :--------: | :------ |
| bonus |double   | the total voting bonus he can receive |
| detail |map\<string, double\>   | the bonus from every candidate |


## /getTokenInfo/{symbol}/{by\_longest\_chain}
---

##### **GET**
**概要:** Query the token information.

### Request

A request may look like this:

```
curl http://127.0.0.1:30001/getTokenInfo/iost/1
```
| Key | Type | Description |
| :----: | :-----: | :------: |
| symbol | string  | token symbol |
| by\_longest\_chain | bool  | true - get data from the longest chain; false - get data from irreversible blocks|

### Response

A successful response may look like this:

```
200 OK
{
	"symbol": "iost",
	"full_name": "iost",
	"issuer": "issue.iost",
	"total_supply": "9000000000000000000",
	"current_supply": "2100000000000000000",
	"decimal": 8,
	"can_transfer": true
}
```

| Key | Type | Description |
| :----: | :--------: | :------ |
| symbol |string   | token symbol |
| full_name |string   | token full name |
| issuer |string   | token issuer |
| total_supply |string   | total amount of token supply |
| current_supply |string   | current amount of token supply |
| decimal | int   | token decimal |
| can_transfer | bool   | whether the token can be transfered |
