In this project we created a POA blockchain network using puppeth and Geth. We started the network and conncetd to MyCrypto account  to send a test transaction.   Here is a brief description of the network configuration along with the instructions on how to restart the network

## Configuration of the "realnet" network
 
The first step in building the network is to create two (2) new nodes.  The account addresses for these nodes will be pre-approved to seal blocks.

Once we had the preapproved sealer addresses, we then generate the genesis block and supplied these addresses in the list of accounts to seal and list of accounts to prefund.

Using "puppeth" to create.  the Genesis block, a password and Chain ID are created. The password will be required to start the network and the chain ID is needed to connect to the"Mycrypto" wallet. Also the Chain-ID, is needed to perform multi-node operations later. In a network, all nodes need to be in the same Chain ID

The Default block time is selected (default 15). This refers to the length of time it takes to create a new block or file in a cryptocurrency chain.

Once this set up is completed, the Genesis configuration is exported to the local directory.  This creates the "realnet.json" file, which will be used to initialize the 
network.

See below for screenshot of Genesis configuration

![puppeth config](realnet/screenshots/puppeth_config.PNG)

![realnet](realnet/screenshots/directory.PNG)

![node 1](realnet/screenshots/node_1.PNG)

Once, the network has been initialized, the nodes can then be used to begin mining blocks.  Following are the instruction to start the network and begin mining:


## Starting the network

In order to start the network, you must have installed, Go Ethereum Tools https://geth.ethereum.org/downloads/

This should be saved in a directory called “Blockchain Tools”

`Node1`

To start Node 1 navigate to "Blockchain Tools" and use the following command:
```
./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
```
 Type the password and hit enter 

* The `--rpc` flag enables us to talk to the node, which will allow us to use MyCrypto  to transact on our chain.

The node should start producing new blocks.. Copy the enode://address, located in the Started P2P Networking line.

`Node2`-

Start Node 2 in a separate terminal, using the following command:
```
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
```
* Port has to be different for each node. Since the first node's sync port used up 30303, we need to use 30304 for node 2

* use the first node's enode address as the bootnode flag. The bootnodes flag allows us to connect both of our nodes.


 * Type the password and hit enter .

You should see Node 2 start producing new blocks

Image of both nodes running

![Both nodes running](realnet/screenshots/both_nodes.PNG)


## Connecting 'realnet" to Mycrypto
Once the nodes are up and running, we can now connect to Mycrpyto.

`step 1`

 Go to Mycrypto, select change network, and add "realnet" as a custom network  by inputting the following information
* Node Name = realnet
* Network Name = realnet
* Currency = ETH
* Chain ID = (ID chosen when creating the Genesis)
* Default URL http://127.0.0.1:8545

`step 2`

Connect to the custome network, and test it by sending money between account
* Got to View & send
* click Keystore file
* Select Wallet File
* Navigate to Node 1 keystore directory on local computer and selcect the file
* Enetr password 

This will open the account wallet inside MyCrypto, revealing the pre-funded balance from the Genesis configuaration.

`step 3`

Send a test transaction.
* To Address = Node 2 account address
* Amount = amount of ETH to be sent 
* Send transaction
* Send
* Check TX Status
Once the status changes from pending to successful, you should see the funds.


### Note to Instructor / TA
As previously discussed, I was unable to connect to Mycrypto.  I tried to add my custom Node however I got the below error message even after rebuilding the network and trying again.

![capture](realnet/screenshots/Capture.PNG)

It seems the network was added, however I am unable to connect to it as shown in below error message

![realnet](realnet/screenshots/realnet.PNG)

![realnet](realnet/screenshots/cant_connect.PNG)

So I was not able to send the test transaction.