# Diseño y Desarrollo I
## PEC 2- Ejercicio 2

En primer lugar, se ha modificado el fichero "index.html" del Truffle Project "Ethereum Pet Shop" realizado durante la PEC 1, contenido en el directorio "src/", para mostrar mi nombre (Álvaro Peñalva) en el frontend de la aplicación. Seguidamente, se ha subido dicho Truffle Project sin la carpeta "node_modules/" al correspondiente [repositorio de GitHub](https://github.com/penalvaperez/DDI-PEC2/tree/master/DDI-PEC2-Ejercicio2/pet-shop-tutorial).

A continuación se ha descargado IPFS del siguiente [link](https://dist.ipfs.io/#go-ipfs), y se ha instalado con el comando mostrado a continuación:

    $ sudo ./install.sh

Una vez instalado, se ha procedido a su inicialización mediante el comando:

    $ ipfs init
    initializing IPFS node at /home/alvaro/.ipfs
    generating 2048-bit RSA keypair...done
    peer identity: QmUFLa1jqRmPnRVRMsQHfHBtLWQcUoKixR1SiFnZHghJ7u
    to get started, enter:
    
    ipfs cat /ipfs/QmS4ustL54uo8FzR9455qaxZwuMiUhyvMcX9Ba8nUH4uVv/readme

En cuanto al proyecto, en primer lugar se procede a lanzar una blockchain a través de Ganache, tal y como puede observarse en la siguiente captura de pantalla:

![Ganache](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio2/Image1.png)

Seguidamente, se procede a migrar los contratos a dicha blockchain en Ganache a través del terminal:

    $ truffle migrate
    
    Compiling your contracts...
    ===========================
    > Compiling ./contracts/Adoption.sol
    > Compiling ./contracts/Migrations.sol
    > Artifacts written to /home/alvaro/Desktop/pet-shop-tutorial_completa/build/contracts
    > Compiled successfully using:
       - solc: 0.5.8+commit.23d335f2.Emscripten.clang
    
    
    Starting migrations...
    ======================
    > Network name:    'development'
    > Network id:      5777
    > Block gas limit: 0x6691b7
    
    
    1_initial_migration.js
    ======================
    
       Replacing 'Migrations'
       ----------------------
       > transaction hash:    0xfb68c45135eed35afe5abf3667bf97afcfe4de7b8165fd83c2057bcd35462ace
       > Blocks: 0            Seconds: 0
       > contract address:    0x0eB43611e6fc1ad874E5726FEF97136E49A89707
       > block number:        1
       > block timestamp:     1562191944
       > account:             0xf234A6FC658E1A51Ef3cD129AC856f00b2143e09
       > balance:             99.99477214
       > gas used:            261393
       > gas price:           20 gwei
       > value sent:          0 ETH
       > total cost:          0.00522786 ETH
    
    
       > Saving migration to chain.
       > Saving artifacts
       -------------------------------------
       > Total cost:          0.00522786 ETH
    
    
    2_deploy_contracts.js
    =====================
    
       Replacing 'Adoption'
       --------------------
       > transaction hash:    0x2bf054041f5776b977656f4dff4f625fc05f9436d39451471cbe8d6a28af6a2f
       > Blocks: 0            Seconds: 0
       > contract address:    0x79BBCCf737BB3de37ba9994A881b54431f96E116
       > block number:        3
       > block timestamp:     1562191945
       > account:             0xf234A6FC658E1A51Ef3cD129AC856f00b2143e09
       > balance:             99.98918034
       > gas used:            237567
       > gas price:           20 gwei
       > value sent:          0 ETH
       > total cost:          0.00475134 ETH
    
    
       > Saving migration to chain.
       > Saving artifacts
       -------------------------------------
       > Total cost:          0.00475134 ETH
    
    
    Summary
    =======
    > Total deployments:   2
    > Final cost:          0.0099792 ETH

En la siguiente captura de pantalla es posible observar cómo se han producido un total de 4 transacciones sobre la primera dirección de Ganache, lo cual ha hecho disminuir su balance:

![Ganache](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio2/Image2.png)

Seguidamente, y con el objetivo de alojar la DApp en IPFS, en primer lugar se mueven a una carpeta "dist/" los ficheros necesarios para su correcto funcionamiento. Tal y como puede observarse en el apartado "baseDir" definido en el fichero bs-config.json, los archivos relevantes se encuentran en las carpetas "src/" y "build/contracts/". Así, pues, se llevan todos estos ficheros a la raíz del nuevo directorio "dist/", teniéndose la siguiente estructura:

    $ cd dist
    $ ls
    Adoption.json  css  fonts  images  index.html  js  Migrations.json  pets.json

Adicionalmente, y teniendo en cuenta que se ha modificado la ruta de numerosos archivos, es necesario editar el fichero app.js para proceder de nuevo a su enrutamiento. Las rutas que deben modificarse son:

 - **pets.json**: pasa de `'../pets.json'` a `'pets.json'`.
 - **Adoption.json**: en este caso su ruta no se modifica, puesto que en ambos casos se encontraba en la raíz de uno de los directorios base.

Finalmente, y para proceder al alojamiento de la DApp en IPFS, se procede a lanzar un daemon:

    $ ipfs daemon
    Initializing daemon...
    go-ipfs version: 0.4.21-
    Repo version: 7
    System version: amd64/linux
    Golang version: go1.12.5
    Swarm listening on /ip4/10.0.2.15/tcp/4001
    Swarm listening on /ip4/127.0.0.1/tcp/4001
    Swarm listening on /ip6/::1/tcp/4001
    Swarm listening on /p2p-circuit
    Swarm announcing /ip4/10.0.2.15/tcp/4001
    Swarm announcing /ip4/127.0.0.1/tcp/4001
    Swarm announcing /ip6/::1/tcp/4001
    API server listening on /ip4/127.0.0.1/tcp/5001
    WebUI: http://127.0.0.1:5001/webui
    Gateway (readonly) server listening on /ip4/127.0.0.1/tcp/8080
    Daemon is ready

Una vez el Daemon está listo, puede realizarse la subida de la DApp a partir del directorio dist recién creado desde otra ventana del terminal:

    $ ipfs add -r dist
    added QmZJUGqi9caCT6E3Qh679Ytn6iLh7AtziWXfUg77aZ7hWp dist/Adoption.json
    added QmPyD9cVcxL2FoVyuYvHs6gicQ4i54BoZtJMqK4JQE22sH dist/Migrations.json
    added QmYUaCPwvJWiueRXFSTTv8vdedWWzRhRdn8RMw35e7k67u dist/css/bootstrap.min.css
    added QmbrzMumAwEPCoLs6jBdDyHz2TBjpkSFhcCHMT7fBsdFyr dist/css/bootstrap.min.css.map
    added QmWhoNhVUb9bcjuKLB259VYogJpPsJaAe8dern9LK95tVN dist/fonts/glyphicons-halflings-regular.eot
    added QmbcbjLEC1aHy4j2qvtncevjenYwHjEF4qZ2kK5pRJzDLg dist/fonts/glyphicons-halflings-regular.svg
    added QmciDEkreBpY2S6Ktg1Zarbsx5K2DmHK59H261Bjr2fnuR dist/fonts/glyphicons-halflings-regular.ttf
    added QmaYEdLkMnEHVN8HZB2GGETottySZoHh3TnYZERke36PVr dist/fonts/glyphicons-halflings-regular.woff
    added QmUbUsBQbjJhm5iYba5jqibRr4A6gG3HVczSy5gs5PrMhY dist/fonts/glyphicons-halflings-regular.woff2
    added QmacvUkwHXqjqaHevcNXRvTHompuCSXgTwFRxp2yWJQJah dist/images/boxer.jpeg
    added QmcCkw63o2kTaMwHhuUtqZ9cqX7rbVGv9wFJD5nwaXkWPv dist/images/french-bulldog.jpeg
    added Qmaj7LUwb7T5sMFyznMGS1cAGPyVJL6Vhjwemq4zb1Nbex dist/images/golden-retriever.jpeg
    added QmT3m9b5UDTr9gKgN1xKQfS5fSKAx8AdZCJ1XJxJTii29m dist/images/scottish-terrier.jpeg
    added QmZBSrqXG8RhiD9SM4sPVPbmPwtnPraztaNAS3TrVeNt1n dist/index.html
    added QmYJPQAPcBbZAPhbHescjUGUDqkSP2Z7SkyaVRAkvEKDro dist/js/app.js
    added QmNXRFREw7waGtKW9uBUze3PkR9E12HeeAQSkZQSiFUJqo dist/js/bootstrap.min.js
    added QmZQp29tbdppjqyixxM8L8NjsG4paN4eVW9GxZYicXov9v dist/js/truffle-contract.js
    added QmdTtsVM7KtvycQ68f9M43N4EQKvbd58q8aeAhP2fMz4Di dist/js/web3.min.js
    added QmZKHAuYoeAjHqfhi2jJaELDfMBj6dtydz7UsZv3BPaon8 dist/pets.json
    added QmQfwrATTrJc1aTN1dVu9K7nQ5rw67np8yg46EvAbqKEZw dist/css
    added Qmb3fJpXVGvUnNeRLC3P5sTXMzjpf5zq4tKt9XjhtYFf1k dist/fonts
    added QmQo4AjSx9JkNsHa3nRqxtryx6iGHmqGprhm2ic2MztW3Y dist/images
    added QmNzxS5xFBr8kpTT5ZcV5D1ZrRUFUohhg78Q3Uqkd6WPBs dist/js
    added QmUqcYRCmQ82V6uXPysRBNRB6iLyDfCyui41ZCvpXAcQaT dist
     1.47 MiB / 1.47 MiB [=================================================]  99.94%

En este caso, la raíz "dist/" lleva asociado el siguiente hash: 

> QmUqcYRCmQ82V6uXPysRBNRB6iLyDfCyui41ZCvpXAcQaT

Puede comprobarse accediendo a los ficheros que contiene:

    $ ipfs ls QmUqcYRCmQ82V6uXPysRBNRB6iLyDfCyui41ZCvpXAcQaT
    QmZJUGqi9caCT6E3Qh679Ytn6iLh7AtziWXfUg77aZ7hWp 49048 Adoption.json
    QmPyD9cVcxL2FoVyuYvHs6gicQ4i54BoZtJMqK4JQE22sH 53948 Migrations.json
    QmQfwrATTrJc1aTN1dVu9K7nQ5rw67np8yg46EvAbqKEZw -     css/
    Qmb3fJpXVGvUnNeRLC3P5sTXMzjpf5zq4tKt9XjhtYFf1k -     fonts/
    QmQo4AjSx9JkNsHa3nRqxtryx6iGHmqGprhm2ic2MztW3Y -     images/
    QmZBSrqXG8RhiD9SM4sPVPbmPwtnPraztaNAS3TrVeNt1n 2554  index.html
    QmNzxS5xFBr8kpTT5ZcV5D1ZrRUFUohhg78Q3Uqkd6WPBs -     js/
    QmZKHAuYoeAjHqfhi2jJaELDfMBj6dtydz7UsZv3BPaon8 2716  pets.json


Por último, una vez alojada la DApp, se comprueba que funciona a través de IPFS de igual manera que en su ejecución local.

Para ello, en primer lugar se comprueba que puede accederse a la misma a través del navegador web, introduciendo la siguiente dirección asociada al explorador IPFS con el hash obtenido para la carpeta raíz "dist/":

> https://ipfs.io/ipfs/QmUqcYRCmQ82V6uXPysRBNRB6iLyDfCyui41ZCvpXAcQaT/

![IPFS](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio2/Image3.png)

Por otro lado, se comprueba igualmente que puede accederse a través del localhost:

> http://localhost:8080/ipfs/QmUqcYRCmQ82V6uXPysRBNRB6iLyDfCyui41ZCvpXAcQaT

![IPFS](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio2/Image4.png)

Finalmente, se realiza lo propio para el acceso desde Gateway:

> http://gateway.ipfs.io/ipfs/QmUqcYRCmQ82V6uXPysRBNRB6iLyDfCyui41ZCvpXAcQaT

![IPFS](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio2/Image5.png)

Por último, se procede a comprobar que la DApp funciona de forma correcta tras ser alojada en IPFS. Para ello, y tal y como puede observarse en la siguiente captura de pantalla, se ha procedido a adoptar a los dos primeros perros, pasando su estado de "Adopt" a "Success" correctamente, y viéndose reducido consecuentemente el balance en la cuenta de Ethereum asociada:

![IPFS](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio2/Image6.png)

Finalmente, en la imagen mostrada a continuación se observa cómo el número de transacciones en Ganache para dicha cuenta se ha visto incrementado en 2:

![IPFS](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio2/Image7.png)



