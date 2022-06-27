What?
--------

Tools for https://komodoplatform.com Notary Nodes

Tested on Ubuntu 18.04, 20.04 and 21.04

**_This set of scripts is interdependent. Any piecemeal usage or mixing with other scripts may result in unexpected behavior!  Please review and understand what the scripts are doing and the data they expect before attempting to use separately from the rest in the repo._**

e.g. the `start` and `assetchains` scripts set the `pid` parameter on the daemons when starting up which is expected to be set when using the `resetwallet` script.

Dependencies (installed during `./init`)
```
sudo apt-get install jq bc dc
```

Setup
--------

* Install Ubuntu 18.04, 20.04 or 21.04
```
cd $HOME
git clone https://github.com/webworker01/freshubuntu
cd freshubuntu && sudo ./freshubuntu
```
* Input full ssh key when prompted, login with a separate terminal using SSH key (should not require password)
```
cd $HOME
git clone https://github.com/webworker01/nntools.git
cd nntools
cp config.example config
nano config
```
 * setup your config
```
./init
./start
```
* Once `init` starts you can `tail -f $HOME/nntools.log` to more easily keep track of progress
* wait til syncs are complete (multiple hours to sync all. you can verify complete with ./stats and see no errors)
```
 komodo-cli importprivkey <privkey>
 ./assets-cli importprivkey <privkey>
 ./asset-cli ltc importprivkey
./checkaddresses
./kmdacfirewall
```
(note the space in front to exclude the privkey commands from your ~/.bash_history)

* Create your [wp_7776 or wp_7779](https://docs.komodoplatform.com/notary/setup-Komodo-Notary-Node.html#create-wp-7776)
```
cd $HOME/nntools

./buildnotary
./startnotary
```

* Create cron jobs `crontab -e`
```
*/10 * * * * /home/ww/nntools/cronsplit
1 * * * * /home/ww/nntools/cronsplit long
7 * * * * /home/ww/nntools/cleanwallettransactions
11 * * * * /home/ww/nntools/collectinterest
```

Scripts
--------

Script Name | Function
----------- | --------
**asset-cli** | Send in a single coin name (1P or 3P) to run RPC commands against
**assets-cli** | Run RPC command against all KMD smartchain coins
**build** | You can run `./build <coinname>` to build/rebuild any already cloned coin repo required for NN
**checkaddresses** | Validate your NN address is imported correctly against all coins
**checkfork** | Script to quickly check all assetchains for possible forks
**checkmasks** | Check your nodes connectivity to the notary node network
**collectall** | Loop and collect every UTXO until all are completely consolidated
**collectinterest** | My method of consolidating mine funds (cronjob)
**cleanwallettransactions** | Runs cleanwallettransactions against all KMD based coins (cronjob)
**cronsplit** | Script to schedule auto splitting of utxos to be used in conjunction with splitfunds (cronjob)
**init** | Clones required repos, sets up sensible default configs and builds them (skips if repo is already cloned)
**kill** | Look up the process id of a komodod and KILL (pkill -9)
**kmdacfirewall** | UFW settings with commentary
**minerfixer** | Tweak to not mine (waste CPU) when node is not eligible for easy-mining (automatically added to komodo.conf if using `init`)
**niceiguana** | Run this to display iguana pids and suggested nice command
**scanresetwallets** | Checks all wallet sizes against the variables in config "size to monitor for in bytes" and runs the appropriate wallet reset script for the coin that is over the limit
**setconfigpermissions** | Finds all `.conf` files in `.komodo` data dir and subdirectories and sets higher security permissions on them (`init` does this by default)
**start** | Start all coins daemons
**startnotary** | Starts dPoW
**stats** | Fancy cli stats for notary nodes
**stop** | Stop all coin daemon
**stopnotary** | Stops dPoW
**transferall** | Transfer kmd and all assetchains to address you specify
**zsend** | Script to simplify sending a specified amount to/from z addressess

Utility Files
---------
File Name | Function
----------- | --------
**assetchains** | Start one or all assetchains (used by `start`)
**c/boost.cpp** | Simple c++ program to verify if boost is installed and return its version
**coinlist** | Handy way to KMD smartchains in one place for other scripts to use, see also `paths`
**config.example** | Copy this to a new file called config and modify as appropriate
**dpow** | Start dpow script (used by `startnotary`)
**functions** | Store functions for use in other files
**functions-wallet** | Store functions for use in other files
**main** | Most if not all scripts include this file to set common variables etc (don't need to run directly)
**networktweaksundo.md** | Reference to my default Ubuntu 16.04 net config "just in case"
**paths** | Stores paths to different coin files
**resetwallet*** | Various reset wallet methods (used by `scanresetwallets`)
**splitfunds** | Split utxo types required for notarizations (used by `cronsplit`)
**7776** | Stores 7776 files so they're out of the way

See Also
----------
https://github.com/webworker01/freshubuntu
