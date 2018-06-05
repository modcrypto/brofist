# Brofist Master Nodes Setup Guide

**Please, update your brofist wallet to the latest version:** https://github.com/modcrypto/brofist/releases

<img src="https://docs.google.com/drawings/d/e/2PACX-1vSxM_rihB5b6L-E5xOknGS-UFovfTpFYIzjSOCWkAbqv4QLYXyADB6wwx6IpUQ-ETzIPLFeHVaT5Qft/pub?w=892&amp;h=453">

## Multi-Level Master Node 
|Tier	| PEW Require	| MN Reward |
|-----|--------------|-----------|
| 1	| 1,250 PEW	  	|   6.67%   |
| 2	| 2,500 PEW	   |	13.33%   |
| 3	| 5,000 PEW	   |	26.67%   |
| 4	| 10,000 PEW	|	53.33%   |
| 5	| 20,000 PEW	|	66.67%   |
| 6	| 50,000 PEW	|	80.00%   |

Send PEW meet the tier required to your MN wallet. It needs 20-30 minutes for transaction confirmation (At least 15 confirms).
You can buy PEW at : https://ubit.pw/markets/brofistbtc  
 
## Two Options for Setting up your Wallet
1. [One GUI wallet control multiple masternodes on VPS.](#option1)
   I recommended this option if you are consolidating wallets
   
2. [Install masternode on GUI Wallet](#option2)
   You need to open the wallet 24/7, and static IPV4.


LINUX Setup Guide
============
* VPS >= 1 GB of RAM, OS : Linux Ubuntu 16.04
* Brofist Wallet https://github.com/modcrypto/brofist/releases 

### 1. Steps to Create a New Sudo User
You can cross this step, if you already have user account.
1. Log in to your VPS server as the root user.
2. Use the adduser command to add a new user to your system.
3. Use the usermod command to add the user to the sudo group.
4. Close the terminal and re-login with your new username.

(You can replace ***brofist*** with the username that you want to create.)
```bash 
adduser brofist
usermod -aG sudo brofist
```

### 2. Prepare the environment for runnning the Brofist wallet
Login with your brofist username.
Please run theses command line by line.
```bash
sudo apt-get update 
sudo apt-get upgrade 
sudo apt-get install git automake build-essential libtool autotools-dev autoconf pkg-config nano software-properties-common
sudo apt-get install libssl-dev libboost-all-dev libevent-dev 
sudo apt-add-repository ppa:bitcoin/bitcoin 
sudo apt-get update 
sudo apt-get install libdb4.8-dev libdb4.8++-dev sudo libminiupnpc-dev libzmq3-dev
```

### 3. Download and Setup the Brofist Core Masternode.
Download the latest file "brofistmaster_ubuntu.x.x.tar.gz"
Example commands:

```bash
wget https://github.com/modcrypto/brofist/releases/download/1.0.2.12/brofist_ubuntu1604_1.0.2.12.tar.gz
tar -xvf brofist_ubuntu1604_1.0.2.12.tar.gz
sudo cp linux/b* /usr/bin 

```

Master Node Setup Guide
============
1. Install new wallet.

You must install one Brofist wallet on each VPS.  
**Each Brofist masternode needs an unique IP address.** 
There are 2 options:  1) brofist-qt (GUI) or 2) brofistd (Daemon No-GUI control via RPC)
 
1.1 For Windows (recommend to use brofist-qt)
- Download  https://github.com/modcrypto/brofist/releases/download/1.0.2.12/brofist-qt_win32_1.0.2.12.zip
- Unzip and Open your QT Wallet : brofist-qt.exe
- Wait Until blockchain and masternode synced.
- Go to Menu: Files/Receiving Address  and copy the resulting wallet address

1.2 For Linux  (recommend to use brofistd) 
- start the wallet daemon with command: 
```  
  brofistd -daemon
```
  and wait until the wallet synce. 
- You can view information of this wallet with the command:
```  
  brofist-cli getinfo 
```
- You can stop the brofist daemon with the command:
```  
  brofist-cli stop
```

1.3 Generate new Brofist wallet address with command:
```  
  brofist-cli getnewaddress master  
```
Copy the resulting wallet address  

2. Goto your main wallet and send the PEW coin to new wallet address in step 1.
Please see the above table for the requirement PEW for each masternode level. 
You needs to wait 20-30 minutes for transaction confirmation (At least 15 confirms).
You can buy PEW at : https://ubit.pw/markets/brofistbtc  

3. Back to your VPS wallet.
- Check for valid masternode output collateral.
```  
  brofist-cli masternode outputs  
```
If your wallet ready to be the masternode, it will return the transaction no output.
For example
```  
{
  "0eeb81a0ad6b67136e868f6a7820dfc922e9fc1edfc746e0a3f080b754aca036": "1"
}
```  
4. Generate Masternode Private Key
```  
  brofist-cli masternode genkey
```
You will get the result like this:
```  
7feWwZmYXdCNmYPVwCCLswnx9YBVweafDPHbTM13KMTSfaJQXEq
```
5. Create or Edit file brofist.conf
For windows, it should is in  C:\Users\<Your Name>\AppData\Roaming\BroFistCore

For LINUX, it should is in  $HOME/.brofistcore

Example : brofist.conf
```  
listen=1
daemon=1
server=1
rpcuser=pew
rpcpassword=password
rpcallowip=127.0.0.1
maxconnections=30
masternode=1
masternodeprivkey=7feWwZmYXdCNmYPVwCCLswnx9YBVweafDPHbTM13KMTSfaJQXEq
```
The masternodeprivkey is copied from the output of step 4.

6. Check your public IP address.

```  
curl ipinfo.io/ip

ifconfig 

```

You will see your **public ip** and  **inet addr**; Both ip must be the same address.
You cannot use the local ip such as 127.x.x.x, 192.168.x or 169.254.x.x  .

7. Create or Edit file masternode.conf

For windows, it should is in  C:\Users\<Your Name>\AppData\Roaming\BroFistCore
For LINUX, it should is in  $HOME/.brofistcore

`masternode.conf` format is a space seperated text file. Each line consisting of an alias, IP address followed by port, masternode private key, collateral output transaction id and collateral output index.

```
alias ipaddress:port masternode_private_key collateral_output collateral_output_index
```

- ipaddress -- from step 6
- port -- must be 11113
- masternode_private_key -- from step 4
- collateral_output and collateral_output_inde -- from step 3

Example:

```
master 172.100.21.85:11113 7feWwZmYXdCNmYPVwCCLswnx9YBVweafDPHbTM13KMTSfaJQXEq 0eeb81a0ad6b67136e868f6a7820dfc922e9fc1edfc746e0a3f080b754aca036 1
```

8. Restart the brofist daemon
```
 brofist-cli stop
# wait for 3 second 
 brofistd -daemon

# wait for 3 minutes
 brofist-cli masternode start-all
 brofist-cli masternode start

# check the masternode status
 brofist-cli masternode status
 brofist-cli masternode list-conf
 
```

## <a name="option1"></a>Setting GUI wallet for control multiple masternodes on VPS.

If you have many VPS, you can control all of them with a Brofist GUI wallet.

1. Dump the private key from your masterNode's pulic key.

- For daemon wallet(Linux), type the command:
```
brofist-cli dumpprivkey [the wallet address]
```
Copy the resulting priviate key. You'll use it in the next step.

### From your multi-instance Masternode Wallet

Open your QT Wallet and go to console (from the menu select `Tools` => `Debug Console`)

Import the private key from the step above.

```
walletpassphrase [your_wallet_passphrase] 600
importprivkey [single_instance_private_key]
```

The wallet will re-scan and you will see your available balance increase by the amount that was in the imported wallet.

[Skip Option 2. and go to Create masternode.conf file](#masternodeconf)

## <a name="option2"></a>Option 2. Starting with a new wallet

[If you used Option 1 above, then you can skip down to Create masternode.conf file.](#masternodeconf)

### Create New Wallet Addresses

1. Open the QT Wallet.
2. Click the Receive tab.
3. Fill in the form to request a payment.
    * Label: mn01
    * Amount: 1000 (optional)
    * Click *Request payment* button
5. Click the *Copy Address* button

Create a new wallet address for each Masternode.

Close your QT Wallet.

### Send 1000 PEW to New Addresses

Just like setting up a standard MN. Send exactly 1000 PEW to each new address created above.

### Create New Masternode Private Keys

Open your QT Wallet and go to console (from the menu select `Tools` => `Debug Console`)

Issue the following:

```masternode genkey```

*Note: A masternode private key will need to be created for each Masternode you run. You should not use the same masternode private key for multiple Masternodes.*

Close your QT Wallet.

## <a name="masternodeconf"></a>Create masternode.conf file

Remember... this is local. Make sure your QT is not running.

Create the `masternode.conf` file in the same directory as your `wallet.dat`.

Copy the masternode private key and correspondig collateral output transaction that holds the 1000 PEW.

The masternode private key may be an existing key from [Option 1](#option1), or a newly generated key from [Option 2](#option2). 

*Note: The masternode priviate key is **not** the same as a wallet private key. **Never** put your wallet private key in the masternode.conf file. That is almost equivalent to putting your 1000 PEW on the remote server and defeats the purpose of a hot/cold setup.*

### Get the collateral output

Open your QT Wallet and go to console (from the menu select `Tools` => `Debug Console`)

Issue the following:

```masternode outputs```

Make note of the hash (which is your collateral_output) and index.

### Enter your Masternode details into your masternode.conf file
[From the brofist github repo](https://github.com/brofistcoin/brofist/blob/master/doc/masternode_conf.md)

`masternode.conf` format is a space seperated text file. Each line consisting of an alias, IP address followed by port, masternode private key, collateral output transaction id and collateral output index.

```
alias ipaddress:port masternode_private_key collateral_output collateral_output_index
```

Example:

```
mn01 127.0.0.1:9999 93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 2bcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a67c 0
mn02 127.0.0.2:9999 93WaAb3htPJEV8E9aQcN23Jt97bPex7YvWfgMDTUdWJvzmrMqey aa9f1034d973377a5e733272c3d0eced1de22555ad45d6b24abadff8087948d4 0
```

## What about the brofist.conf file?

If you are using a `masternode.conf` file you no longer need the `brofist.conf` file. The exception is if you need custom settings (_thanks oblox_). In that case you **must** remove `masternode=1` from local `brofist.conf` file. This option should be used only to start local Hot masternode now.

## Update brofist.conf on server

If you generated a new masternode private key, you will need to update the remote `brofist.conf` files.

Shut down the daemon and then edit the file.

```nano .brofistcore/brofist.conf```

### Edit the masternodeprivkey
If you generated a new masternode private key, you will need to update the `masternodeprivkey` value in your remote `brofist.conf` file.

## Start your Masternodes

### Remote

If your remote server is not running, start your remote daemon as you normally would. 

You can confirm that remote server is on the correct block by issuing

```brofist-cli getinfo```

and comparing with the official explorer at https://explorer.brofist.org/chain/BroFist

### Local

Finally... time to start from local.

#### Open up your QT Wallet

From the menu select `Tools` => `Debug Console`

If you want to review your `masternode.conf` setting before starting Masternodes, issue the following in the Debug Console:

```masternode list-conf```

Give it the eye-ball test. If satisfied, you can start your Masternodes one of two ways.

1. `masternode start-alias [alias_from_masternode.conf]`  
Example ```masternode start-alias mn01```
2. `masternode start-many`

## Verify that Masternodes actually started

### Remote

Issue command `masternode status`
It should return you something like that:
```
brofist-cli masternode status
{
    "vin" : "CTxIn(COutPoint(<collateral_output>, <collateral_output_index>), scriptSig=)",
    "service" : "<ipaddress>:<port>",
    "pubkey" : "<1000 PEW address>",
    "status" : "Masternode successfully started"
}
```
Command output should have "_Masternode successfully started_" in its `status` field now. If it says "_not capable_" instead, you should check your config again.

### Local

Search your Masternodes on https://brofistninja.pl/masternodes.html

_Hint: Bookmark it, you definitely will be using this site a lot._
