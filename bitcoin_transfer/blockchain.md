# Chapter5. Blockchain {#blockchain}

## Section1. Introducing the basic concepts and terms for the Blockchain system Part1 

A Blockchain is composed of blocks. And each block shapes the chain by referencing the previous block. A block is composed of a block header and transaction(s). 

See the illustration depicting a block and a blockchain, drawn by Young-min Park(Youngmtool), in the following link:
https://youngmtool.gitbooks.io/csharpdotnetconceptsandillustrations/blockchain.html

A header is composed of several data such as version(block version information.), prev_block(the hash value of the previous block, being used to reference the previous block.), merkle_root(the reference to a merkle tree collection which is a hash of all transactions related to this block.), timestamp(a timestamp recording when this block was created.), bits(the calculated difficulty target being used for this block.), nonce(the nonce used to generate this block… to allow variations of the header and compute different hashes.), txn_count(number of transaction entries, this value is always 0.).


Now let's see the transaction which is another part of the block along with the header.

The following is the looking of one transaction:  
```json
{
  "hash": "4788c5ef8ffd0463422bcafdfab240f5bf0be690482ceccde79c51cfce209edd",
  "ver": 1,
  "vin_sz": 1,
  "vout_sz": 2,
  "lock_time": 0,
  "size": 259,
  "in": [
    {
      "prev_out": {
        "hash": "a6ae1beb8250a8fa6080749d5f82caee40f741d40957f0e8c4e4cc88830672ad",
        "n": 1
      },
      "scriptSig": "3046022100aa39716861e508ae75ef577b3d83795a78d31cd72af0310b12ef8084cc16c9b8022100da72f62cdbd1b8d41cb4f8090e8c3b2929714279b3570962351dfbb739c2724601 0485c05717a0d35b2931c1395e9dcfffed3e67decff429477c48f6352da314c109ce0074bd1b991dd462ba16dbe9e4227193d35cc9342ea67f1b481054e345eef0"
    },
	{
      "prev_out": {
        "hash": "fbcc98b9601e9498c2ac097a493c6eb20473c438bf84891d572109335792198d",
        "n": 1
      },
      "scriptSig": "3045022100fc8e579f4cabda1e26a294b3f7f227087b64ca2451155b8747bd1f6c96780d6d022041912d38512030e1ec1d3df6b8d91d8b9aa4c564642fd7cafc48f97fd550100101 0482d593f88a39160eaed14470ee4dad283c29e88d9abb904f953115b1a93d6f3881d6f8c29c53ddb30b2d1c6b657068d60a93ed240d5efca247836f6395807bcd"
    },
	{
      "prev_out": {
        "hash": "fbcc98b9601e9498c2ac097a493c6eb20473c438bf84891d572109335792198d",
        "n": 3
      },
      "scriptSig": "3045022100fc8e579f4cabda1e26a294b3f7f227087b64ca2451155b8747bd1f6c96780d6d022041912d38512030e1ec1d3df6b8d91d8b9aa4c564642fd7cafc48f97fd550100101 0482d593f88a39160eaed14470ee4dad283c29e88d9abb904f953115b1a93d6f3881d6f8c29c53ddb30b2d1c6b657068d60a93ed240d5efca247836f6395807bcd"
    }
  ],
  "out": [
    {
      "value": "0.00010000",
      "scriptPubKey": "OP_DUP OP_HASH160 edb82bd321c0c4b2b667c58e28ebc113d9bb38cd OP_EQUALVERIFY OP_CHECKSIG"
    },
    {
      "value": "0.01440000",
      "scriptPubKey": "OP_DUP OP_HASH160 21d77a260a7d8fb1b0064f9e3c0b4e46a44e8199 OP_EQUALVERIFY OP_CHECKSIG"
    }
  ]
}
```
Note that one block can have multiple transactions.

A transaction is composed of several data:  
1.TxIn.  
A TxIn can have input(s). One input is composed of "prev_out" pointing to unspent output located in different transaction by specifying that output with the hash value of that transaction and the index number of that output in the correspond transaction and "scriptSig" playing a role of the signature.  
2. TxOut.  
A TxOut is composed of output(s). One output is composed of the value for an amount of coins which will be sent and a value of ScriptPubKey.  
3. Other minimal data.  
(1)hash is a transaction ID which is generated by twice hashing the entire of transaction(TxOut, TxIn, other minimal data)  
(2)ver indicates the version of the transaction.  
(3)vin_sz indicates the size of the TxIn.  
(4)vout_sz indicates the size of the TxOut.  
(5)lock_time  
(6)size indicates the entire size of the transaction.


## Section2. Introducing the basic concepts and terms for the Blockchain system Part2

And each whole Blockchain located in each computer is termed by the ledger. And also each computer participating in the Bitcoin system network, with running the Bitcoin application and the whole blockchain which is termed the ledger, is termed the node.  

And among the nodes, particular nodes which make the block by gathering transactions generated and transferred by the Bitcoin system clients, are termed the miner. And as of writing this book, the block should be created every average 10 minutes. Sometimes the block is created in 6 minutes after the previous block had been created. Somtimes the block is created in 13 minutes after the previous block had been created. It means that it's the average 10 minutes. And the 10 minutes which is one of protocols is for Bitcoin blockchain system. Other kinds of blockchain system can have different protocols as to this time. This particular 10 minutes which is needed to create a new block is specified for some purposes such as sustaining a stability of the Bitcoin system, preventing malcious attempts from being happened too frequently and so on.  

And miner nodes compete to create the bloack and to append that bloack to the main chain. The block not appended into the main chain is termed the orphaned block. You only be able to get the coin from the coinbase transaction which is the first transaction of the newly created block and to get the mining fees generated by each transaction made by other Bitcoin system clients, in the block newly created by the corresponding miner who is getting fees in this block.


## Section3. More on the Blockchain system

You might have noticed that while we proved ownership of the unspent TxOut. And even more, prior to mentioning the proof of the ownership, note that we have not yet proven the TxOut actually exists. This is where the main function of the Blockchain shines:

The Blockchain is the database of all transactions that have happened since the the first Bitcoin transaction, known as the Genesis block. The Blockchain is duplicated all around the world. If you use Bitcoin Core, you have the whole Blockchain on your computer. Once a transaction appears on the Blockchain, it is very easy to prove its existence.

**Miners** are entities whose only goal is to insert a transaction in The Blockchain. However miners do not modify the blockchain everytime they receive one transaction. Instead each of them try to add a whole batch of transactions at the same time in something known as a **block**. Other nodes on the network confirm the new block obeys the rules set forth in the Bitcoin protocol. If two miners add a block at the same time, we have a **fork**, but ultimately only the branch of the fork with the most **work** will be continued. If a miner tries to include an invalid transaction in his block, the other nodes will not recognize it and the miner loses the investment spent on creating the block.

Once a miner manages to submit a valid block, all transactions inside are considered **Confirmed**. When this happens all miners must discard their current work and begin working on a new block using new transactions. When a block is confirmed it is added to the Blockchain as the most recent block. The likelihood of this addition being undone decreases dramatically with every subsequent block that is added on top of it.

For the first time in history we have a database which can’t easily be rewritten, eliminates the need for trust, resists censorship, and is widely distributed. Comparing the Blockchain to a ledger is only relevant if we consider Bitcoin as a currency.

The Blockchain is a database, and you give meaning to its data. As you will soon discover, a bitcoin transaction can bear more information than just bitcoin transfers. A bitcoin transaction is a row in a database that can never be erased.

As a user, you can verify that a specific transaction exists in the Blockchain in two different ways:

*   Check the entire Blockchain, which at the time of this writing is several gigabytes in size.
*   Ask for a partial Merkel tree, which are a few kilobytes in size. We will talk about merkel trees later in relation to Simple Payment Verification.


Ref.  
https://en.bitcoin.it/wiki/Protocol_documentation#Block_Headers
