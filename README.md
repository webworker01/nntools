What?
--------

Tools for https://komodoplatform.com Notary Nodes

Assumes Ubuntu 18 installation (might work with 16)

Setup
--------

This set of scripts is interdependent. Any piecemeal usage or mixing with other scripts may result in unexpected behavior!  Please review and understand what the scripts are doing and the data they expect before attempting to use separately from the rest in the repo. 

e.g. the `start` and `assetchains` scripts set the `pid` parameter on the daemons when starting up which is expected to be set when using the `resetwallet` script.

Dependencies
```
sudo apt-get install jq bc dc
```

Copy the `config.example` file to `config` and edit as needed. No further edits in the various files should be required.

Scripts
--------

Script Name | Function
----------- | --------
**asset-cli** | Send in a single coin name to run RPC commands against
**assetchains** | Start one or all assetchains
**assets-cli** | Run RPC command against all coins in coinlist
**checkaddresses** | Validate address against all coins in coinlist
**checkfork** | Script to quickly check all assetchains for possible forks
**checkmasks** | Check your nodes connectivity to the notary node network
**cronsplit** | Script to schedule auto splitting of utxos to be used in conjunction with splitfunds
**dpow** | Start dpow
**importkey** | Import privkey to all assetchains without rescan
**init** | Clones required repos and builds them
**kmdacfirewall** | UFW settings with commentary
**minerfixer** | Tweak to not mine (waste CPU) when node is not eligible for easy-mining
**splitfunds** | Use to split utxo types required for notarizations
**start** | Start coins daemons as defined by `thirdpartycoins` in config
**stats** | Fancy cli stats for notary nodes
**stop** | Stop coins daemons as defined by `thirdpartycoins` in config
**transferall** | Transfer kmd and all assetchains to address you specify
**zsend** | Script to simplify sending a specified amount to/from z addressess

Utility Files
---------
File Name | Function
----------- | --------
**coinlist** | Handy way to keep coin list in one place for other scripts to use (thanks to a-team)
**config.example** | Copy this to a new file called config and modify as appropriate
**functions** | Store functions for use in other files
**networktweaksundo.txt** | Reference to my default Ubuntu 16.04 net config "just in case"
**paths** | Stores paths to different coin files
**rebuild*** | Files to rebuild coin daemons that have already been cloned
**7776** | Stores ready to execute 7776 files

See Also
----------
https://github.com/webworker01/freshubuntu
