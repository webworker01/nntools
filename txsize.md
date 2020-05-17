# Sapling Raw Transaction Hex

To calculate the size of a transaction in bytes, get the hex string with `getrawtransaction` and divide by 2.

Before the transaction is signed, we do not know the hex of the actual transaction, so here I attempt to estimate. Some strings I have not yet identified and simply have marked as "unknown".

See [calcFee](https://github.com/webworker01/nntools/blob/master/functions#L51) for a simplified bash implementation.

* tx version                  8
* versiongroupid              8
* numberofinputs              2
* vins:     (p2pkh=296,p2pk=228)
    * txid                    64
    * vout #                  8
    * unknown                 2
    * scriptsig:
        * p2pkh               214
        * p2pk                146
    * unknown ffffffff        8
* numberofoutputs             2
* vouts:      (p2pkh=70,p2pk=88)
    * p2pk:
        * value               16
        * unknown 2321        4
        * pubkey              66
        * unknown ac          2
    * p2pkh
        * unknown             2
        * value               16
        * unknown 1976a914    8
        * ripemd160           40
        * unknown 88ac        4
* nlocktime                   8
* end sapling                 30
