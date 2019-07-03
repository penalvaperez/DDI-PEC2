# Diseño y Desarrollo I

## PEC 2- Ejercicio 1

En primer lugar se debe realizar la sincronización completa del nodo de Rinkeby. Para ello, se lanza dicho nodo en modo "fast" debido a los problemas de estabilidad y escasa existencia de peers en modo "light" a través del siguiente comando:

    $ geth --rinkeby --datadir=./rinkeby --syncmode "fast" --rpc --rpcapi db,eth,net,web3,personal --cache=1024 --rpcport 8545 --rpcaddr 127.0.0.1 --rpccorsdomain "*"
    INFO [07-03|20:56:16.694] Maximum peer count                       ETH=25 LES=0 total=25
    INFO [07-03|20:56:17.095] Starting peer-to-peer node               instance=Geth/v1.8.27-stable-4bcc0a37/linux-amd64/go1.10.4
    INFO [07-03|20:56:17.106] Allocated cache and file handles         database=/home/alvaro/.ethereum/rinkeby/geth/chaindata cache=512 handles=2048
    INFO [07-03|20:57:06.731] Persisted trie from memory database      nodes=355 size=51.91kB time=3.373591ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
    INFO [07-03|20:57:07.012] Initialised chain configuration          config="{ChainID: 4 Homestead: 1 DAO: <nil> DAOSupport: true EIP150: 2 EIP155: 3 EIP158: 3 Byzantium: 1035301 Constantinople: 3660663  ConstantinopleFix: 4321234 Engine: clique}"
    INFO [07-03|20:57:07.292] Initialising Ethereum protocol           versions="[63 62]" network=4
    INFO [07-03|20:57:08.251] Loaded most recent local header          number=1249003 hash=fee04f…a53daa td=2428378 age=1y7mo3w
    INFO [07-03|20:57:08.251] Loaded most recent local full block      number=0       hash=6341fd…67e177 td=1       age=2y3mo2d
    INFO [07-03|20:57:08.251] Loaded most recent local fast block      number=1238758 hash=702384…76df92 td=2407920 age=1y7mo3w
    INFO [07-03|20:57:08.339] Loaded local transaction journal         transactions=0 dropped=0
    INFO [07-03|20:57:08.339] Upgrading chain index                    type=bloombits percentage=33
    INFO [07-03|20:57:08.339] Regenerated local transaction journal    transactions=0 accounts=0
    INFO [07-03|20:57:18.608] New local node record                    seq=6 id=982092c5a869c0c6 ip=127.0.0.1 udp=30303 tcp=30303
    INFO [07-03|20:57:19.115] Started P2P networking                   self=enode://bfc2e39b1579bd73002cd50792878b2223b0b86c28152efc149171ee4926388b5001c88da2bbc2094f80e1ffbc39733a6ffb90b8bf43c19d5105d7b89b05fbaf@127.0.0.1:30303
    INFO [07-03|20:57:20.832] IPC endpoint opened                      url=/home/alvaro/.ethereum/rinkeby/geth.ipc
    INFO [07-03|20:57:21.003] Upgrading chain index                    type=bloombits percentage=33
    INFO [07-03|20:57:21.346] HTTP endpoint opened                     url=http://127.0.0.1:8545                   cors=* vhosts=localhost
    INFO [07-03|20:57:29.116] Block synchronisation started 
    INFO [07-03|20:57:29.589] Upgrading chain index                    type=bloombits percentage=35
    INFO [07-03|20:57:34.909] Imported new block headers               count=0 elapsed=398.895ms number=1238950 hash=d1a8f7…1047d1 age=1y7mo3w ignored=192
    INFO [07-03|20:57:35.027] Imported new block headers               count=0 elapsed=105.813ms number=1239142 hash=5dbdcd…098a83 age=1y7mo3w ignored=192
    INFO [07-03|20:57:35.052] Imported new block receipts              count=2 elapsed=779.418µs number=1238760 hash=b4ac1d…21b912 age=1y7mo3w size=3.75kB
    INFO [07-03|20:57:35.187] Imported new block receipts              count=32 elapsed=7.177ms   number=1238792 hash=c79f96…598886 age=1y7mo3w size=87.08kB
    INFO [07-03|20:57:35.382] Imported new block headers               count=0  elapsed=327.596ms number=1239718 hash=90f8b0…d1a688 age=1y7mo3w ignored=576
    INFO [07-03|20:57:35.512] Imported new block headers               count=0  elapsed=104.355ms number=1239910 hash=850e05…23e9c0 age=1y7mo3w ignored=192
    INFO [07-03|20:57:35.617] Imported new block receipts              count=159 elapsed=204.851ms number=1238951 hash=9a19e2…46ab91 age=1y7mo3w size=243.30kB
    INFO [07-03|20:57:35.674] Imported new block receipts              count=191 elapsed=50.582ms  number=1239142 hash=5dbdcd…098a83 age=1y7mo3w size=595.63kB
    INFO [07-03|20:57:35.956] Imported new block headers               count=0   elapsed=420.712ms number=1240294 hash=76947d…5bf16d age=1y7mo3w ignored=384
    INFO [07-03|20:57:35.982] Imported new block receipts              count=109 elapsed=28.867ms  number=1239251 hash=f1401b…ed5c22 age=1y7mo3w size=260.20kB
    INFO [07-03|20:57:36.037] Imported new block receipts              count=157 elapsed=48.566ms  number=1239408 hash=e9b08b…68bd54 age=1y7mo3w size=441.33kB
    INFO [07-03|20:57:36.125] Imported new block headers               count=0   elapsed=122.781ms number=1240486 hash=900ab4…9028fe age=1y7mo3w ignored=192
    INFO [07-03|20:57:36.236] Imported new block receipts              count=144 elapsed=48.483ms  number=1239552 hash=1930af…10a713 age=1y7mo3w size=401.10kB

Tras esto, en un terminal diferente, y con el objetivo de poder interactuar con la red Rinkeby, se vincula la consola JavaScript de Geth:

    $ geth attach ipc:/home/alvaro/Desktop/rinkeby/geth.ipc

A través de esta consola puede consultarse, por ejemplo, el estado de la red:

    > net
    {
      listening: true,
      peerCount: 1,
      version: "4",
      getListening: function(callback),
      getPeerCount: function(callback),
      getVersion: function(callback)
    }

A continuación, y mientras se sincroniza la red Rinkeby, se procede a importar el fichero "ensutils-rinkeby.js", necesario para realizar el proceso de forma directa. En este caso, ya se han cambiado los dos ENS necesarios en la línea correspondiente. La consola devuelve un valor booleano afirmativo tras la carga:

    > loadScript("./ensutils-rinkeby.js")
    true

En este caso, y tras unas 7 horas de sincronización, la red Rinkeby se encuentra prácticamente sincronizada. No obstantante, se utiliza el siguiente comando para comprobarlo:

    > eth.syncing
    {
      currentBlock: 4670074,
      highestBlock: 4670155,
      knownStates: 8983489,
      pulledStates: 8969633,
      startingBlock: 4670050
    }

Si se compara este valor con el mostrado en la siguiente imagen de la web [Etherscan.io](https://rinkeby.etherscan.io/) para la red Rinkeby, los bloques se encuentran extremadamente parejos:

![Etherscan.io](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio1/Image1.png)

No obstante, el proceso no ha finalizado todavía, puesto que la sincronización de los estados continúa. Este proceso puede llegar a ser incluso más largo que la propia sincronización de los bloques, pudiendo incluso no llegar a completarse nunca en el caso de la utilización de un HDD en lugar de un SDD, tal y como se describe en el siguiente [link](https://github.com/ethereum/go-ethereum/issues/16282).

Analizando el log del nodo se comprueba que, efectivamente, la mayor parte de la sincronización que está realizándose ahora es la de los estados: 

    INFO [07-03|21:44:07.886] Imported new state entries               count=219  elapsed=2.863ms   processed=9122934 pending=1307  retry=0 duplicate=2 unexpected=620
    INFO [07-03|21:44:12.333] Imported new state entries               count=655  elapsed=6.550ms   processed=9123589 pending=1261  retry=0 duplicate=2 unexpected=620
    INFO [07-03|21:44:17.340] Imported new state entries               count=702  elapsed=14.859ms  processed=9124291 pending=1068  retry=0 duplicate=2 unexpected=620
    INFO [07-03|21:44:20.419] Imported new state entries               count=477  elapsed=4.868ms   processed=9124768 pending=1074  retry=0 duplicate=2 unexpected=620
    INFO [07-03|21:44:24.022] Imported new block headers               count=1    elapsed=2.440ms   number=4670215 hash=008e30…53914d
    INFO [07-03|21:44:24.333] Imported new state entries               count=495  elapsed=4.490ms   processed=9125263 pending=3051  retry=0 duplicate=2 unexpected=620
    INFO [07-03|21:44:36.365] Imported new state entries               count=1743 elapsed=25.609ms  processed=9127006 pending=2253  retry=0 duplicate=2 unexpected=620

Lamentablemente, si se trata de continuar con el proceso de registro de dominio sin que el nodo Rinkeby haya finalizado la sincronización tanto de estados como de bloques, la consola arroja un error. A continuación puede comprobarse dicho fenómeno mediante la utilización del comando correspondiente a la comprobación del registro previo de un determinado dominio:

    > testRegistrar.expiryTimes(web3.sha3("penalvaperez-rinkeby"))
    Error: invalid address
        at web3.js:3930:15
        at web3.js:3734:22
        at web3.js:5025:28
        at map (<native code>)
        at web3.js:5024:12
        at web3.js:5050:18
        at web3.js:5075:23
        at web3.js:4102:22
        at apply (<native code>)
        at web3.js:4227:12

Sin embargo, y hasta que se complete la mencionada sincronización, se describirá el procedimiento a seguir para realizar el registro de un dominio.

Tal y como ya se ha indicado, el siguiente comando comprueba si el dominio indicado, en este caso "penalvaperez-rinkeby", se encuentra previamente registrado. Si el valor temporal devuelto es 0 o negativo, entonces el dominio está disponible.

    > testRegistrar.expiryTimes(web3.sha3("penalvaperez-rinkeby"))

Una vez se ha dado con un dominio disponible, es posible proceder a su dominio con el siguiente comando, el cual vincula la primera cuenta Ethereum previamente creada, obtenida desde `eth.accounts[0]`:

    > testRegistrar.register(web3.sha3("penalvaperez-rinkeby"), eth.accounts[0], {from: eth.accounts[0]})

En caso exitoso, y tras esperar a que la blockchain incluya la transacción, la consola devolverá el hash de la misma. Para confirmar que, efectivamente, el dominio ha quedado registrado, es posible volver a ejecutar el siguiente comando, el cual deberá devolver ahora un número positivo:

    > testRegistrar.expiryTimes(web3.sha3("penalvaperez-rinkeby"))

De igual forma, si se ejecuta el comando mostrado a continuación, la consola devolverá la cuenta de Ethereum introducida anteriormente:

    > ens.owner(namehash("penalvaperez-rinkeby.test"))

 A partir de este instante ya se posee el dominio ".test" en la red Rinkeby, pero todavía no se resuelve en nada. Para ello puede crearse un resolver propio, o tomar uno de la red. En este caso se ha hecho uso del siguiente, [propiedad de Michal Zalecki ](https://gist.github.com/MichalZalecki/db02810da8e582d0494adb2c5fd31f3c):

> 0x5d20cf83cb385e06d2f2a892f9322cd4933eacdc

Se ejecuan así los siguientes comandos con el objetivo de asignar el resolver indicado al dominio y cuenta anteriormente registrados: 

    > publicResolver = resolverContract.at("0x5d20cf83cb385e06d2f2a892f9322cd4933eacdc")
    > ens.setResolver(namehash("penalvaperez-rinkeby.test"), publicResolver.address, {from: eth.accounts[0]})

En caso de éxito, la consola devolverá la dirección correspondiente.

De igual forma, puede comprobarse de la siguiente manera que el dominio mantiene el resolver asignado, observando cómo la consola devuelve la misma dirección que fue introducida:

    > ens.resolver(namehash("penalvaperez-rinkeby.test"))
    "0x5d20cf83cb385e06d2f2a892f9322cd4933eacdc"

Finalmente, sería posible asignar el dominio, por ejemplo, a la cuenta Ethereum propia anteriormente mencionada. Para ello sería necesario hacer uso del siguiente comando:

    > publicResolver.setAddr(namehash("penalvaperez-rinkeby.test"), eth.accounts[0], {from: eth.accounts[0]})
    
En caso de que la asignación resulte exitosa, los siguientes comandos devolverían la dirección Ethereum asignada:

    > getAddr(""penalvaperez-rinkeby.test")
    > publicResolver.addr(namehash(""penalvaperez-rinkeby.test"))

