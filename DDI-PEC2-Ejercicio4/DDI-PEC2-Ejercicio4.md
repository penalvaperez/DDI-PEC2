# Diseño y Desarrollo I

## PEC 2- Ejercicio 4

En primer lugar, en este ejercicio se va a crear la primera de las cuentas generada en ejercicios anteriores para la red de pruebas Rinkeby. Tal y como puede observarse en la consola Geth, esta cuenta es la siguiente:

    > eth.accounts[0]
    "0x50fbbd40a6f1910471eae6ed850ffd07d223314b"
    > eth.coinbase
    "0x50fbbd40a6f1910471eae6ed850ffd07d223314b"

Seguidamente, y con el objetivo de poder realizar y firmar las transacciones de la DApp, se va a proceder a vincular esta cuenta, creada en Geth, con MetaMask. Para ello se hará uso de la herramienta MyEtherWallet, siendo necesario obtener primeramente la clave Privada de la cuenta a partir del correspondiente fichero Keystore UTC generado por Geth.

Así, en la siguiente captura de pantalla puede observarse el fichero Keystore buscado, cuyo nombre incluye la dirección de la cuenta seleccionada anteriormente:

![Keystore](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio4/Image1.png)

A continuación debe introducirse la contraseña de la cuenta y proceder con el desbloqueo mediante el botón "Unlock":

![MyEtherWallet](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio4/Image2.png)

Una vez desbloqueada es posible consultar ciertos detalles de la cuenta, entre los que se encuentra la correspondiente clave privada. Seguidamente se importa la cuenta en MetaMask mediante la utilización de dicha clave privada en la red Rinkeby:

![MetaMask](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio4/Image3.png)

No obstante, y tal y como puede observarse, la cuenta posee un balance nulo. Por lo tanto, se procede a realizar una solicitud de fondos a través de la web [Rinkeby Authenticated Faucet](https://faucet.rinkeby.io/), utilizando Twitter como red social de verificación:

![MetaMask](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio4/Image4.png)

Una vez la cuenta creada en Geth está vinculada a MetaMask y cuenta con los fondos necesarios, se procede a migrar los contratos a Rinkeby. Para ello, en primer lugar es necesario editar el fichero "truffle-config.js", añadiendo la red "rinkeby" en "networks" con la cuenta utilizada:

    module.exports = {
      // See <http://truffleframework.com/docs/advanced/configuration>
      // for more about customizing your Truffle configuration!
      networks: {
        development: {
          host: "127.0.0.1",
          port: 7545,
          network_id: "*" // Match any network id
        },
        develop: {
          port: 8545
        },
        rinkeby: {
          host: "localhost", // Connect to geth on the specified
          port: 8545,
          from: "0x50fbbd40a6F1910471eAe6ed850ffd07D223314b", // default address to use for any transaction Truffle makes during migrations
          network_id: 4,
          gas: 4612388 // Gas limit used for deploys
        }
      }
    };

A continuación se procede a iniciar el nodo Rinkeby desbloqueando la cuenta utilizada con el objetivo de poder interactuar con ella. Como puede observarse, es necesario introducir la contraseña de dicha cuenta:

    $ geth --rinkeby --datadir=./rinkeby --syncmode "fast" --rpc --rpcapi db,eth,net,web3,personal --cache=1024 --rpcport 8545 --rpcaddr 127.0.0.1 --rpccorsdomain "*" --unlock="0x50fbbd40a6F1910471eAe6ed850ffd07D223314b"
    INFO [07-04|19:46:35.909] Maximum peer count                       ETH=25 LES=0 total=25
    INFO [07-04|19:46:35.915] Starting peer-to-peer node               instance=Geth/v1.8.27-stable-4bcc0a37/linux-amd64/go1.10.4
    INFO [07-04|19:46:35.915] Allocated cache and file handles         database=/home/alvaro/Desktop/rinkeby/geth/chaindata cache=512 handles=2048
    INFO [07-04|19:46:37.280] Persisted trie from memory database      nodes=355 size=51.91kB time=4.047194ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
    INFO [07-04|19:46:37.281] Initialised chain configuration          config="{ChainID: 4 Homestead: 1 DAO: <nil> DAOSupport: true EIP150: 2 EIP155: 3 EIP158: 3 Byzantium: 1035301 Constantinople: 3660663  ConstantinopleFix: 4321234 Engine: clique}"
    INFO [07-04|19:46:37.281] Initialising Ethereum protocol           versions="[63 62]" network=4
    INFO [07-04|19:46:37.393] Loaded most recent local header          number=4675496 hash=370a61…7d6315 td=8560272 age=2m23s
    INFO [07-04|19:46:37.394] Loaded most recent local full block      number=0       hash=6341fd…67e177 td=1       age=2y3mo3d
    INFO [07-04|19:46:37.394] Loaded most recent local fast block      number=4675413 hash=76d3eb…10ec1f td=8560106 age=23m8s
    INFO [07-04|19:46:37.394] Loaded local transaction journal         transactions=0 dropped=0
    INFO [07-04|19:46:37.394] Regenerated local transaction journal    transactions=0 accounts=0
    INFO [07-04|19:46:38.193] New local node record                    seq=19 id=c0a2eadef9f745a3 ip=127.0.0.1 udp=30303 tcp=30303
    INFO [07-04|19:46:38.194] Started P2P networking                   self=enode://46a1987f667fe6035b8806048e800afab2cba8afd5ff9857b1994545045911dee8627e350e584f7316ec8ed986689a776fdcd31798ba4c233f7da577d81be178@127.0.0.1:30303
    INFO [07-04|19:46:38.200] IPC endpoint opened                      url=/home/alvaro/Desktop/rinkeby/geth.ipc
    INFO [07-04|19:46:38.200] HTTP endpoint opened                     url=http://127.0.0.1:8545                 cors=* vhosts=localhost
    Unlocking account 0x50fbbd40a6F1910471eAe6ed850ffd07D223314b | Attempt 1/3
    Passphrase: 
    INFO [07-04|19:46:46.844] Unlocked account                         address=0x50fbbd40a6F1910471eAe6ed850ffd07D223314b
    INFO [07-04|19:47:08.198] Block synchronisation started 
    INFO [07-04|19:47:12.221] Imported new block headers               count=9 elapsed=437.502ms number=4675505 hash=5df104…6aa3a1 ignored=83
    INFO [07-04|19:47:12.328] Imported new block receipts              count=2 elapsed=1.741ms   number=4675415 hash=6bf1d3…94c706 age=23m13s  size=22.44kB
    INFO [07-04|19:47:12.688] Imported new block receipts              count=27 elapsed=13.973ms  number=4675442 hash=c38a0f…263747 age=16m28s  size=252.47kB
    INFO [07-04|19:47:15.008] Imported new block headers               count=1  elapsed=981.072µs number=4675506 hash=dbd164…5678c1
    INFO [07-04|19:47:19.517] New local node record                    seq=20 id=c0a2eadef9f745a3 ip=83.41.57.214 udp=53169 tcp=30303
    INFO [07-04|19:47:30.723] Imported new block headers               count=1  elapsed=6.124ms   number=4675507 hash=941ce7…6220ac
    INFO [07-04|19:47:46.450] Imported new block headers               count=1  elapsed=767.709µs number=4675508 hash=7b7da5…9b3e46
    INFO [07-04|19:47:51.092] Imported new state entries               count=630 ela

Finalmente, puede procederse a migrar los contratos mediante el siguiente comando:

    $ truffle migrate --network rinkeby

En este caso, la consola informa del siguiente error, debido a que el nodo no ha completado la sincronización con la red Rinkeby:

    Compiling your contracts...
    ===========================
    > Everything is up to date, there is nothing to compile.
    
    
    Migrations dry-run (simulation)
    ===============================
    > Network name:    'rinkeby-fork'
    > Network id:      4
    > Block gas limit: 0x47b760
    
    
    1_initial_migration.js
    ======================
    
       Deploying 'Migrations'
       ----------------------
    Error: Error: Error:  *** Deployment Failed ***
    
    "Migrations" could not deploy due to insufficient funds
       * Account:  0x50fbbd40a6F1910471eAe6ed850ffd07D223314b
       * Balance:  0 wei
       * Message:  sender doesn't have enough funds to send tx. The upfront cost is: 9224776000000000 and the sender's account only has: 0
       * Try:
          + Using an adequately funded account
          + If you are using a local Geth node, verify that your node is synced.
    
        at Object.run (/usr/lib/node_modules/truffle/build/webpack:/packages/truffle-migrate/index.js:92:1)
        at <anonymous>
        at process._tickCallback (internal/process/next_tick.js:189:7)
    Truffle v5.0.24 (core: 5.0.24)
    Node v8.16.0

En este caso, sucede algo similar a lo ocurrido en el Ejercicio 1: como el nodo no se encuentra completamente sincronizado por culpa de los estados, tal y como puede observarse a continuación:

    > eth.syncing
    {
      currentBlock: 4675572,
      highestBlock: 4675671,
      knownStates: 37756941,
      pulledStates: 37751521,
      startingBlock: 4675413
    }

Como consecuencia, el balance de la cuenta tampoco se encuentra actualizado y, por lo tanto, no existen fondos suficientes para desplegar el contrato:

    > eth.getBalance(eth.coinbase)
    0

No obstante, a continuación se describirán los pasos a seguir cuando el nodo se encuentre sincronizado completamente y el contrato se haya migrado de forma correcta.

Así, en este caso se toma como punto de partida el final del Ejercicio 1, en el cual se había procedido a asignar un resolver en Rinkeby al dominio "penalvaperez-rinkeby.test" y cuenta utilizada:

    > ens.resolver(namehash("penalvaperez-rinkeby.test"))
    "0x5d20cf83cb385e06d2f2a892f9322cd4933eacdc"

A continuación se lanza una instancia de Swarm:

    swarm --bzzaccount 7686a5f970f276dbcdc0f0de84fb0fad3ef1dea1

Seguidamente, se procede a subir a Swarm la el directorio "dist/", el cual contiene la build de la DApp realizada en el Ejercicio 2, indicando que el archivo "index.html" debe ser abierto de forma predeterminada:

    $ swarm --defaultpath index.html --recursive up dist
    cc771a353f1a3261576465b4c21fab0f1f6c50f1afdfcad0d4bd479ab0f63cd3

A continuación se asigna el resolver y dominio anteriormente indicados a este directorio en Swarm, añadiendo "0x" previamente a su hash:

    publicResolver.setContent(namehash('penalvaperez-rinkeby.test'), "0xcc771a353f1a3261576465b4c21fab0f1f6c50f1afdfcad0d4bd479ab0f63cd3",{from:eth.accounts[0]})

Por último, se lanza una nueva instancia de Swarm vinculada a la red Rinkeby en la cual se ha desplegado el ENS:

    $ swarm --bzzaccount 7686a5f970f276dbcdc0f0de84fb0fad3ef1dea1 --ens-api "/home/alvaro/Desktop/rinkeby/geth.ipc"

Así, la DApp podría ser consultada y utilizada en el navegador a través de las siguientes direcciones:

> http://localhost:8500/bzz:/cc771a353f1a3261576465b4c21fab0f1f6c50f1afdfcad0d4bd479ab0f63cd3

> http://localhost:8500/bzz:/penalvaperez-rinkeby.test/


