![Brofist Logo](/src/qt/res/icons/bitcoin.png)

BROFIST COIN - A COMMUNITY RE-DESIGNED COIN 

What is BroFist?
----------------

I make this fork to look after it, and make it to be the community stable and reliable coin.

- Maximum Supply: 31,000,000 coins
- Algorithm: NeoScrypt
- Type: PoW + MasterNode (Multi-Levels 1250,2500,5000,10000,20000,50000 )
- Coin name: BroFist Coin
- Coin abbreviation: PEW
- Block Time Average: 120 sec
- Block Reward: 0-150 - 1 PEW, 150-250 - 3 PEW, 250+ - 12 PEW. 
- Block Reward Distribution: 6 PEW to Masternodes, 6 PEW to Miners
- Premine: 1% (300,000 PEW with [Ex-Developer] https://github.com/brofistnetwork/brofist )
- Port P2P:***11113** RPC:**12454***

Tools
-------------
* Website: http://www.brofist.online 
* Official Pool : http://pool.brofist.online/
* Block Explorer : http://explorer.brofist.online/
* Bitcointalk ANN : https://bitcointalk.org/index.php?topic=3943730.msg37670155

* Exchange: 
  - Graviex - https://graviex.net/markets/pewbtc
  - BarterDEX - https://komodoplatform.com/decentralized-exchange/
    To use BarterDEX, you must set **rpcport=12454** in brofist.conf 

* Discord: (New) https://discord.gg/QBTgeMZ


How to Update Your Masternode
------------------------
1. Close your BroFist wallet.
2. Download the latest version of Brofist wallet.
3. Delete everything from the folder <USER_FOLDER>\AppData\Roaming\BroFistCore (for windows), 
   EXCEPT wallet.dat, brofist.conf, masternode.conf and backup folder.

![Sample Screen](/doc/brofist_doc/step1.png)

Be extremely careful not to delete wallet.dat, or you may loose all your coins.

4. Then you need to remove addnode that are 100% sure on the right chain to your brofist.conf file :
```ini
maxconnections=30

```
Please don't make maxconnections number higher than 30, or you might desync again.

5. Open your BroFist wallet again.

Master Node Guide
----------------
* [Setting Multiple Masternodes on Ubuntu VPS](https://github.com/modcrypto/brofist/blob/master/doc/masternode_multi.md)


License
-------

BroFist Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is meant to be stable. Development is normally done in separate branches.
[Tags](https://github.com/brofistcoin/brofist/tags) are created to indicate new official,
stable release versions of BroFist Core.

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](/doc/unit-tests.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/qa) are installed) with: `qa/pull-tester/rpc-tests.py`

The Travis CI system makes sure that every pull request is built for Windows
and Linux, OS X, and that unit and sanity tests are automatically run.

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.
