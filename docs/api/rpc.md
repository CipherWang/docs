---
id: rpc
title: JSON-RPC Commands
---



This RPC API document is compatible with `ckb 0.18.0 (rylai-v7 ecd88dc 2019-08-10)`. For more versions of this document, please refer to the [GitHub repo](https://github.com/nervosnetwork/ckb/blob/master/rpc/README.md) directly. 

<!-- Todo update rpc document -->

[Here](https://gist.github.com/Mine77/cb26558a993088a298a2bc1862bb9662) is a `paw` file you can use to import into Rest API softwares such as [Postman](https://www.getpostman.com/)

> The RPC port of your CKB node can be set in your [node configuration](https://github.com/nervosnetwork/ckb/blob/develop/docs/configure.md) file. By default, it uses port 8114.

## An Example
You can interact with your CKB node client via RPC port. Here's an example showing how to get the header information of the tip block (the latest block).

Open a new terminal, and use this command to get the tip block header (note that you should have the `ckb run` running):
```bash
curl -d '{"id": 2, "jsonrpc": "2.0", "method":"get_tip_header","params": []}' -H 'content-type:application/json' 'http://localhost:8114'
```

> Note that you need to have [curl](https://www.google.com/search?q=how+to+install+curl+on+linux) installed.

<details>
<summary>(click here to view response)</summary>
```json
{
    "jsonrpc":"2.0",
    "result":{
        "difficulty":"0x1000",
        "epoch":"0",
        "hash":"0x7ab75ce1a45f30a6fe0d83856aa56827243c88271f4b8e2f968809b175fa2e7e",
        "number":"227",
        "parent_hash":"0xc1b02d64c8a294f1bc935706655213314926d33f031e84fe97fc601559aae9b1",
        "proposals_hash":"0x0000000000000000000000000000000000000000000000000000000000000000",
        "seal":{
            "nonce":"12843279316432878493",
            "proof":"0xa1060000d51100007b130000fd16000031200000982b0000fd370000d757000071730000dc740000a3790000a37b0000"
            },
        "timestamp":"1558138968104",
        "transactions_root":"0xc7067232dc4b44d393b50cea57635a642193963ac19ee3f5385940b2c23a5073",
        "uncles_count":"0",
        "uncles_hash":"0x0000000000000000000000000000000000000000000000000000000000000000",
        "version":"0",
        "witnesses_root":"0x822916ce5ad8b248f5ce549139c456abfdbba3ea3d2a8642c55da706876d0734"
        },
    "id":2
}
```
</details>

## Chain

### `get_block`

Returns the information about a block by hash.

#### Parameters

    hash - Hash of a block

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_block",
    "params": [
        "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "header": {
            "dao": "0x0100000000000000005827f2ba13b000d77fa3d595aa00000061eb7ada030000",
            "difficulty": "0x7a1200",
            "epoch": "1",
            "hash": "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6",
            "number": "1024",
            "parent_hash": "0x4a3492111a90c31564290d070ca216ba416712eff48ab122e050e253e6069281",
            "proposals_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "seal": {
                "nonce": "0",
                "proof": "0x"
            },
            "timestamp": "1557311767",
            "transactions_root": "0x07f8c6e6874b20ad721397af259036af40c8ab22a1bec2fdbeda2c5f489b3d43",
            "uncles_count": "0",
            "uncles_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "version": "0",
            "witnesses_root": "0x0fb9a555e2ae1192ba76b4149a7a01d11df2251229a80de35c49e37d0b0a4407"
        },
        "proposals": [],
        "transactions": [
            {
                "deps": [],
                "hash": "0x07f8c6e6874b20ad721397af259036af40c8ab22a1bec2fdbeda2c5f489b3d43",
                "inputs": [
                    {
                        "previous_output": {
                            "block_hash": null,
                            "cell": null
                        },
                        "since": "1024"
                    }
                ],
                "outputs": [
                    {
                        "capacity": "70193197506",
                        "data_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                        "lock": {
                            "args": [],
                            "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                            "hash_type": "Data"
                        },
                        "type": null
                    }
                ],
                "outputs_data": [
                    "0x"
                ],
                "version": "0",
                "witnesses": [
                    {
                        "data": [
                            "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a500"
                        ]
                    }
                ]
            }
        ],
        "uncles": []
    }
}
```

### `get_block_by_number`

Get block by number

#### Parameters

    block_number - Number of a block

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_block_by_number",
    "params": [
        "1024"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "header": {
            "dao": "0x0100000000000000005827f2ba13b000d77fa3d595aa00000061eb7ada030000",
            "difficulty": "0x7a1200",
            "epoch": "1",
            "hash": "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6",
            "number": "1024",
            "parent_hash": "0x4a3492111a90c31564290d070ca216ba416712eff48ab122e050e253e6069281",
            "proposals_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "seal": {
                "nonce": "0",
                "proof": "0x"
            },
            "timestamp": "1557311767",
            "transactions_root": "0x07f8c6e6874b20ad721397af259036af40c8ab22a1bec2fdbeda2c5f489b3d43",
            "uncles_count": "0",
            "uncles_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "version": "0",
            "witnesses_root": "0x0fb9a555e2ae1192ba76b4149a7a01d11df2251229a80de35c49e37d0b0a4407"
        },
        "proposals": [],
        "transactions": [
            {
                "deps": [],
                "hash": "0x07f8c6e6874b20ad721397af259036af40c8ab22a1bec2fdbeda2c5f489b3d43",
                "inputs": [
                    {
                        "previous_output": {
                            "block_hash": null,
                            "cell": null
                        },
                        "since": "1024"
                    }
                ],
                "outputs": [
                    {
                        "capacity": "70193197506",
                        "data_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                        "lock": {
                            "args": [],
                            "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                            "hash_type": "Data"
                        },
                        "type": null
                    }
                ],
                "outputs_data": [
                    "0x"
                ],
                "version": "0",
                "witnesses": [
                    {
                        "data": [
                            "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a500"
                        ]
                    }
                ]
            }
        ],
        "uncles": []
    }
}
```

### `get_block_hash`

Returns the hash of a block in the best-block-chain by block number; block of No.0 is the genesis block.

#### Parameters

    block_number - Number of a block

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_block_hash",
    "params": [
        "1024"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6"
}
```

### `get_cellbase_output_capacity_details`

Returns each component of the created CKB in this block's cellbase, which is issued to a block N - 1 - ProposalWindow.farthest, where this block's height is N.

#### Parameters

    hash - Block hash

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_cellbase_output_capacity_details",
    "params": [
        "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "primary": "69444444445",
        "proposal_reward": "0",
        "secondary": "748753061",
        "total": "70193197506",
        "tx_fee": "0"
    }
}
```

### `get_cells_by_lock_hash`

Returns the information about cells collection by the hash of lock script.

#### Parameters

    lock_hash - Cell lock script hash
    from - Start block number
    to - End block number

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_cells_by_lock_hash",
    "params": [
        "0xa6ed2edad0d48a3d58d0bec407ddf2e40ddd5f533d7059a160149f4021c2a589",
        "0",
        "2"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": [
        {
            "capacity": "125000000000",
            "lock": {
                "args": [],
                "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                "hash_type": "Data"
            },
            "out_point": {
                "block_hash": "0x1092b58382e225498b5c7263633e0ef4a6d1c34fe9c014cd3cd4afc059bd1dff",
                "cell": {
                    "index": "0",
                    "tx_hash": "0xbf9377613dd3861366f7c14005eebff4abcfdf7e5cc643daec0af5ba249e8c49"
                }
            }
        },
        {
            "capacity": "125000000000",
            "lock": {
                "args": [],
                "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                "hash_type": "Data"
            },
            "out_point": {
                "block_hash": "0x6014787e7aa9a238678ec08157cd4a8f1415775a376f27b0599e9c87df88078e",
                "cell": {
                    "index": "0",
                    "tx_hash": "0x41b03d8cd94134943148224ef8076eaa7417768e9f745f9b14ae4a68fbfd91b5"
                }
            }
        }
    ]
}
```

### `get_current_epoch`

Returns the information about the current epoch.


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_current_epoch",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "difficulty": "0x7a1200",
        "length": "1800",
        "number": "1",
        "start_number": "1000"
    }
}
```

### `get_epoch_by_number`

Return the information corresponding the given epoch number.

#### Parameters

    epoch_number - Epoch number

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_epoch_by_number",
    "params": [
        "0"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "difficulty": "0x3e8",
        "length": "1000",
        "number": "0",
        "start_number": "0"
    }
}
```

### `get_header`

Returns the information about a block header by hash.


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_header",
    "params": [
        "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "dao": "0x0100000000000000005827f2ba13b000d77fa3d595aa00000061eb7ada030000",
        "difficulty": "0x7a1200",
        "epoch": "1",
        "hash": "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6",
        "number": "1024",
        "parent_hash": "0x4a3492111a90c31564290d070ca216ba416712eff48ab122e050e253e6069281",
        "proposals_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "seal": {
            "nonce": "0",
            "proof": "0x"
        },
        "timestamp": "1557311767",
        "transactions_root": "0x07f8c6e6874b20ad721397af259036af40c8ab22a1bec2fdbeda2c5f489b3d43",
        "uncles_count": "0",
        "uncles_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "version": "0",
        "witnesses_root": "0x0fb9a555e2ae1192ba76b4149a7a01d11df2251229a80de35c49e37d0b0a4407"
    }
}
```

### `get_header_by_number`

Returns the information about a block header by block number.


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_header_by_number",
    "params": [
        "1024"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "dao": "0x0100000000000000005827f2ba13b000d77fa3d595aa00000061eb7ada030000",
        "difficulty": "0x7a1200",
        "epoch": "1",
        "hash": "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6",
        "number": "1024",
        "parent_hash": "0x4a3492111a90c31564290d070ca216ba416712eff48ab122e050e253e6069281",
        "proposals_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "seal": {
            "nonce": "0",
            "proof": "0x"
        },
        "timestamp": "1557311767",
        "transactions_root": "0x07f8c6e6874b20ad721397af259036af40c8ab22a1bec2fdbeda2c5f489b3d43",
        "uncles_count": "0",
        "uncles_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "version": "0",
        "witnesses_root": "0x0fb9a555e2ae1192ba76b4149a7a01d11df2251229a80de35c49e37d0b0a4407"
    }
}
```

### `get_live_cell`

Returns the information about a cell by out_point. If <block_hash> is not specific, returns the cell if it is live. If <block_hash> is specified, return the live cell only if the corresponding block contain this cell

#### Parameters

    out_point - OutPoint object {{"tx_hash": <tx_hash>, "index": <index>}, "block_hash": <block_hash>}.

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_live_cell",
    "params": [
        {
            "block_hash": null,
            "cell": {
                "index": "0",
                "tx_hash": "0xf9cab0387e48d97b6905b54a8f647a5803ced1c4f187360fba0ddad292e618e7"
            }
        }
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "cell": {
            "capacity": "34400000000",
            "data_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
            "lock": {
                "args": [],
                "code_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "hash_type": "Data"
            },
            "type": null
        },
        "status": "live"
    }
}
```

### `get_tip_block_number`

Returns the number of blocks in the longest blockchain.


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_tip_block_number",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": "1024"
}
```

### `get_tip_header`

Returns the information about the tip header of the longest.


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_tip_header",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "dao": "0x0100000000000000005827f2ba13b000d77fa3d595aa00000061eb7ada030000",
        "difficulty": "0x7a1200",
        "epoch": "1",
        "hash": "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6",
        "number": "1024",
        "parent_hash": "0x4a3492111a90c31564290d070ca216ba416712eff48ab122e050e253e6069281",
        "proposals_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "seal": {
            "nonce": "0",
            "proof": "0x"
        },
        "timestamp": "1557311767",
        "transactions_root": "0x07f8c6e6874b20ad721397af259036af40c8ab22a1bec2fdbeda2c5f489b3d43",
        "uncles_count": "0",
        "uncles_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "version": "0",
        "witnesses_root": "0x0fb9a555e2ae1192ba76b4149a7a01d11df2251229a80de35c49e37d0b0a4407"
    }
}
```

### `get_transaction`

Returns the information about a transaction requested by transaction hash.

#### Parameters

    hash - Hash of a transaction

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_transaction",
    "params": [
        "0xd295c063a5f99c5c9a05c9a10567956f3fdde834d7a326a13e9c0cac15000649"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "transaction": {
            "deps": [
                {
                    "block_hash": null,
                    "cell": {
                        "index": "0",
                        "tx_hash": "0xf9cab0387e48d97b6905b54a8f647a5803ced1c4f187360fba0ddad292e618e7"
                    }
                }
            ],
            "hash": "0xd295c063a5f99c5c9a05c9a10567956f3fdde834d7a326a13e9c0cac15000649",
            "inputs": [
                {
                    "previous_output": {
                        "block_hash": null,
                        "cell": {
                            "index": "0",
                            "tx_hash": "0xbf9377613dd3861366f7c14005eebff4abcfdf7e5cc643daec0af5ba249e8c49"
                        }
                    },
                    "since": "0"
                }
            ],
            "outputs": [
                {
                    "capacity": "100000000000",
                    "data_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "lock": {
                        "args": [],
                        "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                        "hash_type": "Data"
                    },
                    "type": null
                }
            ],
            "outputs_data": [
                "0x"
            ],
            "version": "0",
            "witnesses": []
        },
        "tx_status": {
            "block_hash": null,
            "status": "pending"
        }
    }
}
```

## Experiment

### `_compute_script_hash`

Returns script hash of given transaction script

**Deprecated**: will be removed in a later version

#### Parameters

    args - Hex encoded arguments passed to reference cell
    code_hash - Code hash of referenced cell
    hash_type - Data: code_hash matches against dep cell data hash; Type: code_hash matches against dep cell type hash.

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "_compute_script_hash",
    "params": [
        {
            "args": [],
            "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
            "hash_type": "Data"
        }
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": "0xa6ed2edad0d48a3d58d0bec407ddf2e40ddd5f533d7059a160149f4021c2a589"
}
```

### `_compute_transaction_hash`

Return the transaction hash

**Deprecated**: will be removed in a later version

#### Parameters

    transaction - The transaction object
    version - Transaction version
    deps - Dependent cells
    inputs - Transaction inputs
    outputs - Transaction outputs
    witnesses - Witnesses

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "_compute_transaction_hash",
    "params": [
        {
            "deps": [
                {
                    "block_hash": null,
                    "cell": {
                        "index": "0",
                        "tx_hash": "0xf9cab0387e48d97b6905b54a8f647a5803ced1c4f187360fba0ddad292e618e7"
                    }
                }
            ],
            "inputs": [
                {
                    "previous_output": {
                        "block_hash": null,
                        "cell": {
                            "index": "0",
                            "tx_hash": "0xbf9377613dd3861366f7c14005eebff4abcfdf7e5cc643daec0af5ba249e8c49"
                        }
                    },
                    "since": "0"
                }
            ],
            "outputs": [
                {
                    "capacity": "100000000000",
                    "data_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "lock": {
                        "args": [],
                        "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                        "hash_type": "Data"
                    },
                    "type": null
                }
            ],
            "outputs_data": [
                "0x"
            ],
            "version": "0",
            "witnesses": []
        }
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": "0xd295c063a5f99c5c9a05c9a10567956f3fdde834d7a326a13e9c0cac15000649"
}
```

### `dry_run_transaction`

Dry run transaction and return the execution cycles.

This method will not check the transaction validity, but only run the lock script
and type script and then return the execution cycles.
Used to debug transaction scripts and query how many cycles the scripts consume


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "dry_run_transaction",
    "params": [
        {
            "deps": [
                {
                    "block_hash": null,
                    "cell": {
                        "index": "0",
                        "tx_hash": "0xf9cab0387e48d97b6905b54a8f647a5803ced1c4f187360fba0ddad292e618e7"
                    }
                }
            ],
            "inputs": [
                {
                    "previous_output": {
                        "block_hash": null,
                        "cell": {
                            "index": "0",
                            "tx_hash": "0xbf9377613dd3861366f7c14005eebff4abcfdf7e5cc643daec0af5ba249e8c49"
                        }
                    },
                    "since": "0"
                }
            ],
            "outputs": [
                {
                    "capacity": "100000000000",
                    "data_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "lock": {
                        "args": [],
                        "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                        "hash_type": "Data"
                    },
                    "type": null
                }
            ],
            "outputs_data": [
                "0x"
            ],
            "version": "0",
            "witnesses": []
        }
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "cycles": "12"
    }
}
```

## Indexer

### `deindex_lock_hash`

Remove index for live cells and transactions by the hash of lock script.

#### Parameters

    lock_hash - Cell lock script hash

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "deindex_lock_hash",
    "params": [
        "0xa6ed2edad0d48a3d58d0bec407ddf2e40ddd5f533d7059a160149f4021c2a589"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": null
}
```

### `get_live_cells_by_lock_hash`

Returns the live cells collection by the hash of lock script.

#### Parameters

    lock_hash - Cell lock script hash
    page - Page number
    per - Page size, max value is 50
    reverse_order - Returns the live cells collection in reverse order, an optional parameter, default is false

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_live_cells_by_lock_hash",
    "params": [
        "0xa6ed2edad0d48a3d58d0bec407ddf2e40ddd5f533d7059a160149f4021c2a589",
        "0",
        "2"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": [
        {
            "cell_output": {
                "capacity": "125000000000",
                "data_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "lock": {
                    "args": [],
                    "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                    "hash_type": "Data"
                },
                "type": null
            },
            "created_by": {
                "block_number": "1",
                "index": "0",
                "tx_hash": "0xbf9377613dd3861366f7c14005eebff4abcfdf7e5cc643daec0af5ba249e8c49"
            }
        },
        {
            "cell_output": {
                "capacity": "125000000000",
                "data_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "lock": {
                    "args": [],
                    "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                    "hash_type": "Data"
                },
                "type": null
            },
            "created_by": {
                "block_number": "2",
                "index": "0",
                "tx_hash": "0x41b03d8cd94134943148224ef8076eaa7417768e9f745f9b14ae4a68fbfd91b5"
            }
        }
    ]
}
```

### `get_lock_hash_index_states`

Get lock hash index states


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_lock_hash_index_states",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": [
        {
            "block_hash": "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6",
            "block_number": "1024",
            "lock_hash": "0xa6ed2edad0d48a3d58d0bec407ddf2e40ddd5f533d7059a160149f4021c2a589"
        }
    ]
}
```

### `get_transactions_by_lock_hash`

Returns the transactions collection by the hash of lock script. Returns empty array when the `lock_hash` has not been indexed yet.

#### Parameters

    lock_hash - Cell lock script hash
    page - Page number
    per - Page size, max value is 50
    reverse_order - Return the transactions collection in reverse order, an optional parameter, default is false

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_transactions_by_lock_hash",
    "params": [
        "0xa6ed2edad0d48a3d58d0bec407ddf2e40ddd5f533d7059a160149f4021c2a589",
        "0",
        "2"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": [
        {
            "consumed_by": null,
            "created_by": {
                "block_number": "1",
                "index": "0",
                "tx_hash": "0xbf9377613dd3861366f7c14005eebff4abcfdf7e5cc643daec0af5ba249e8c49"
            }
        },
        {
            "consumed_by": null,
            "created_by": {
                "block_number": "2",
                "index": "0",
                "tx_hash": "0x41b03d8cd94134943148224ef8076eaa7417768e9f745f9b14ae4a68fbfd91b5"
            }
        }
    ]
}
```

### `index_lock_hash`

Create index for live cells and transactions by the hash of lock script.

#### Parameters

    lock_hash - Cell lock script hash
    index_from - Create an index from starting block number (exclusive), an optional parameter, null means starting from tip and 0 means starting from genesis

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "index_lock_hash",
    "params": [
        "0xa6ed2edad0d48a3d58d0bec407ddf2e40ddd5f533d7059a160149f4021c2a589",
        "1024"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "block_hash": "0x285619ad541bb0be5990c52c9d9d3affc2edaf98100eb3d10117c107761244c6",
        "block_number": "1024",
        "lock_hash": "0xa6ed2edad0d48a3d58d0bec407ddf2e40ddd5f533d7059a160149f4021c2a589"
    }
}
```

## Net

### `get_banned_addresses`

Returns all banned IPs/Subnets.


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_banned_addresses",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": [
        {
            "address": "192.168.0.2/32",
            "ban_reason": "",
            "ban_until": "1840546800000",
            "created_at": "1562803123000"
        }
    ]
}
```

### `get_peers`

Returns the connected peers information.


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_peers",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": [
        {
            "addresses": [
                {
                    "address": "/ip4/192.168.0.3/tcp/8115",
                    "score": "1"
                }
            ],
            "is_outbound": true,
            "node_id": "QmaaaLB4uPyDpZwTQGhV63zuYrKm4reyN2tF1j2ain4oE7",
            "version": "unknown"
        },
        {
            "addresses": [
                {
                    "address": "/ip4/192.168.0.4/tcp/8113",
                    "score": "255"
                }
            ],
            "is_outbound": false,
            "node_id": "QmRuGcpVC3vE7aEoB6fhUdq9uzdHbyweCnn1sDBSjfmcbM",
            "version": "unknown"
        },
        {
            "addresses": [],
            "node_id": "QmUddxwRqgTmT6tFujXbYPMLGLAE2Tciyv6uHGfdYFyDVa",
            "version": "unknown"
        }
    ]
}
```

### `local_node_info`

Returns the local node information.


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "local_node_info",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "addresses": [
            {
                "address": "/ip4/192.168.0.2/tcp/8112/p2p/QmTRHCdrRtgUzYLNCin69zEvPvLYdxUZLLfLYyHVY3DZAS",
                "score": "255"
            },
            {
                "address": "/ip4/0.0.0.0/tcp/8112/p2p/QmTRHCdrRtgUzYLNCin69zEvPvLYdxUZLLfLYyHVY3DZAS",
                "score": "1"
            }
        ],
        "is_outbound": null,
        "node_id": "QmTRHCdrRtgUzYLNCin69zEvPvLYdxUZLLfLYyHVY3DZAS",
        "version": "0.0.0"
    }
}
```

### `set_ban`

Insert or delete an IP/Subnet from the banned list

#### Parameters

    address - The IP/Subnet with an optional netmask (default is /32 = single IP)
    command - `insert` to insert an IP/Subnet to the list, `delete` to delete an IP/Subnet from the list
    ban_time - Time in milliseconds how long (or until when if [absolute] is set) the IP is banned, optional parameter, null means using the default time of 24h
    absolute - If set, the `ban_time` must be an absolute timestamp in milliseconds since epoch, optional parameter
    reason - Ban reason, optional parameter

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "set_ban",
    "params": [
        "192.168.0.2",
        "insert",
        "1840546800000",
        true,
        "set_ban example"
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": null
}
```

## Pool

### `send_transaction`

Send new transaction into transaction pool

If <block_hash> of <previsous_output> is not specified, loads the corresponding input cell. If <block_hash> is specified, load the corresponding input cell only if the corresponding block exist and contain this cell as output.

#### Parameters

    transaction - The transaction object
    version - Transaction version
    deps - Dependent cells
    inputs - Transaction inputs
    outputs - Transaction outputs
    witnesses - Witnesses

#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "send_transaction",
    "params": [
        {
            "deps": [
                {
                    "block_hash": null,
                    "cell": {
                        "index": "0",
                        "tx_hash": "0xf9cab0387e48d97b6905b54a8f647a5803ced1c4f187360fba0ddad292e618e7"
                    }
                }
            ],
            "inputs": [
                {
                    "previous_output": {
                        "block_hash": null,
                        "cell": {
                            "index": "0",
                            "tx_hash": "0xbf9377613dd3861366f7c14005eebff4abcfdf7e5cc643daec0af5ba249e8c49"
                        }
                    },
                    "since": "0"
                }
            ],
            "outputs": [
                {
                    "capacity": "100000000000",
                    "data_hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "lock": {
                        "args": [],
                        "code_hash": "0x28e83a1277d48add8e72fadaa9248559e1b632bab2bd60b27955ebc4c03800a5",
                        "hash_type": "Data"
                    },
                    "type": null
                }
            ],
            "outputs_data": [
                "0x"
            ],
            "version": "0",
            "witnesses": []
        }
    ]
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": "0xd295c063a5f99c5c9a05c9a10567956f3fdde834d7a326a13e9c0cac15000649"
}
```

### `tx_pool_info`

Return the transaction pool information


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "tx_pool_info",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "last_txs_updated_at": "0",
        "orphan": "0",
        "pending": "1",
        "proposed": "0",
        "total_tx_cycles": "12",
        "total_tx_size": "181"
    }
}
```

## Stats

### `get_blockchain_info`

Return state info of blockchain


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_blockchain_info",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": {
        "alerts": [
            {
                "id": "42",
                "message": "An example alert message!",
                "notice_until": "2524579200000",
                "priority": "1"
            }
        ],
        "chain": "main",
        "difficulty": "0x7a1200",
        "epoch": "1",
        "is_initial_block_download": true,
        "median_time": "1557311762"
    }
}
```

### `get_peers_state`

Deprecating in 0.12.0: Return state info of peers


#### Examples

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_peers_state",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

```json
{
    "id": 2,
    "jsonrpc": "2.0",
    "result": [
        {
            "blocks_in_flight": "86",
            "last_updated": "1557289448237",
            "peer": "1"
        }
    ]
}
```