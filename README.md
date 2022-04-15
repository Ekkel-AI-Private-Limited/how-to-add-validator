# how-to-add-validator

  
## Step 1: Create a new address for mining

1.  SSH into the system hosting the non-mining node.
    
2.  Find the datadir for your geth instances. (For nodes being maintained by Ekkel, it is usually /var/cred/.zenith. For nodes being maintained by Zenith, it is usually /var/zenith/.zenith. To confirm, you can ls in the directory and you should find 2 directories called geth and keystore). path_to_directory mentioned in later steps is the path to the datadir and path_to_ipc_file is this path + "geth.ipc"
    
3.  Run the following command to create a new account: geth account new –datadir <path_to_directory>. Save the passphrase and address.
    
<br>    

## Step 2: Vote for this address to become a miner

You will need >50% of validators to vote for this address.

1.  SSH into the system hosting a mining node.
    
2.  Refer to point 2 from step 1 again
    
3.  Run the following command: 
`geth attach <path_to_geth_ipc> --exec 'clique.propose("your_new_address", true)'`
    
4.  Repeat the above steps for >50% of the current validators/miners. You can confirm the number of validators by running the following command: 
`geth attach <path_to_geth_ipc> --exec 'clique.getSigners().length'`
    
<br>
  

## Step 3: Enable mining for the new address

1.  To confirm whether your address has been allowed to become a miner, run the command from point 4 of the last step to confirm whether length has gone up by 1. Also you can run that same command without the “.length” at the end and find your address in the list of miners that gets printed.    

2. Attach geth console to the non-mining node from step 1 where you created the account: 
`geth attach <path_to_geth_ipc>`
    
3.  personal.unlockAccount(). You will require the passphrase from when you created the account.
    
4.  miner.start()
    

  
<br><br>  

Note: Mining/Validating is used interchangeably. There’s technically no “mining” in PoA, but geth commands still call it mining.
