# Diseño y Desarrollo I

## PEC 2- Ejercicio 3

En primer lugar se procede a instalar Swarm en Ubuntu, tal y como se indica en la propia [documentación](https://swarm-guide.readthedocs.io/en/latest/installation.html):

    $ sudo apt-get install ethereum-swarm
    Reading package lists... Done
    Building dependency tree       
    Reading state information... Done
    The following NEW packages will be installed:
      ethereum-swarm
    0 upgraded, 1 newly installed, 0 to remove and 362 not upgraded.
    Need to get 7.190 kB of archives.
    After this operation, 28,4 MB of additional disk space will be used.
    Get:1 http://ppa.launchpad.net/ethereum/ethereum/ubuntu bionic/main amd64 ethereum-swarm amd64 0.4.2+build5368+bionic [7.190 kB]
    Fetched 7.190 kB in 6s (1.189 kB/s)                                            
    Selecting previously unselected package ethereum-swarm.
    (Reading database ... 178524 files and directories currently installed.)
    Preparing to unpack .../ethereum-swarm_0.4.2+build5368+bionic_amd64.deb ...
    Unpacking ethereum-swarm (0.4.2+build5368+bionic) ...
    Setting up ethereum-swarm (0.4.2+build5368+bionic) ...

A continuación se procede a iniciar un nodo de Swarm, para lo cual se crea una nueva cuenta de Ethereum:

    $ geth account new
    INFO [07-03|19:41:24.212] Maximum peer count                       ETH=25 LES=0 total=25
    Your new account is locked with a password. Please give a password. Do not forget this password.
    Passphrase: 
    Repeat passphrase: 
    Address: {7686a5f970f276dbcdc0f0de84fb0fad3ef1dea1}

Se conecta Swarm:

    $ swarm --bzzaccount 7686a5f970f276dbcdc0f0de84fb0fad3ef1dea1
    INFO [07-03|19:42:52.190] Maximum peer count                       ETH=50 LES=0 total=50
    Unlocking swarm account 0x7686a5f970f276DBcdC0F0de84Fb0FaD3ef1DEa1 [1/3]
    Passphrase: 
    INFO [07-03|19:43:04.823] Starting peer-to-peer node               instance=swarm/v0.4.2-3cdc45ee/linux-amd64/go1.11.5
    INFO [07-03|19:43:04.936] New local node record                    seq=1 id=4fe46416a920f108 ip=127.0.0.1 udp=30399 tcp=30399
    INFO [07-03|19:43:04.937] Started P2P networking                   self=enode://3e4022160a428b3225c83d632a9984be591a0c34443bc0dc6430f5c191e166806fc44cd92d5362ef46a06e6269da4b906e5bb1dd50f1ab60d7f20622442be9cc@127.0.0.1:30399
    INFO [07-03|19:43:04.937] Updated bzz local addr                   oaddr=11bd3cb7937c953c100f34fa6eff71b27a116e53fb599d6223ada4f8fc782af8 uaddr=enode://3e4022160a428b3225c83d632a9984be591a0c34443bc0dc6430f5c191e166806fc44cd92d5362ef46a06e6269da4b906e5bb1dd50f1ab60d7f20622442be9cc@127.0.0.1:30399
    INFO [07-03|19:43:04.937] Starting bzz service 
    INFO [07-03|19:43:04.937] Starting hive                            baseaddr=11bd3cb7
    INFO [07-03|19:43:04.937] Detected an existing store. trying to load peers 
    INFO [07-03|19:43:04.937] hive 11bd3cb7: no persisted peers found 
    INFO [07-03|19:43:04.937] Swarm network started                    bzzaddr=11bd3cb7937c953c100f34fa6eff71b27a116e53fb599d6223ada4f8fc782af8
    INFO [07-03|19:43:04.937] Started Pss 
    INFO [07-03|19:43:04.937] Loaded EC keys                           pubkey=0x040c6642c79f4b9b4fe4710b41855390ac3c0eb33e82ce3e9d6c27fd705d2f0340c531cde7f0777e80750996690060ee941c734b2a1439fad3a9edd085758d98a1 secp256=0x030c6642c79f4b9b4fe4710b41855390ac3c0eb33e82ce3e9d6c27fd705d2f0340
    INFO [07-03|19:43:04.937] Streamer started 
    INFO [07-03|19:43:04.941] IPC endpoint opened                      url=/home/alvaro/.ethereum/bzzd.ipc
    INFO [07-03|19:43:09.760] New local node record                    seq=2 id=4fe46416a920f108 ip=83.50.134.243 udp=51210 tcp=30399

Se comprueba que el nodo local de Swarm está corriendo mediante el acceso a través del navegador a la siguiente dirección por defecto:

> http://localhost:8500/

A lo que la consola responde:

    INFO [07-03|19:50:22.486] created ruid for request                 ruid=6ab7aec9 method=GET url=/
    INFO [07-03|19:50:22.486] respondHTML                              ruid=6ab7aec9 code=200
    INFO [07-03|19:50:22.487] request served                           ruid=6ab7aec9 code=200 time=415.298µs
    INFO [07-03|19:50:23.542] created ruid for request                 ruid=c234827d method=GET url=/favicon.ico
    INFO [07-03|19:50:23.542] request served                           ruid=c234827d code=200 time=104.705µs

Tal y como puede observarse en la siguiente captura de pantalla, la conexión es correcta:

![Swarm](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio3/Image1.png)

A continuación se procede a realizar la subida de los archivos correspondientes a la web básica. En este caso, todos ellos se encuentran alojados en el directorio dirWeb/, en el cual existen tres ficheros:

 - **index.html**: en este caso, y tal y como se muestra seguidamente, las rutas de los ficheros deben ser relativas con el objetivo de mantener el mismo hash para el directorio completo, siendo este constante al navegar entre los archivos:

    	<HEAD>
    		<TITLE>WEB</TITLE>
    	</HEAD>
    	<BODY>
    		<ul>
    		  <li><a href="./Doc1.txt">Documento 1</a> Álvaro Peñalva Pérez</li>
    		  <li><a href="./Doc2.txt">Documento 2</a> Álvaro Peñalva Pérez</li>
    		</ul>
    	</BODY>

 - **Doc1.txt**: contiene el texto "Este es el primer documento."
 - **Doc2.txt**: contiene el texto "Este es el segundo documento."

Para llevar a cabo la subida, se emplea el siguiente comando:

    $ swarm --defaultpath index.html --recursive up --encrypt dirWeb

En este caso, se han utilizado los siguientes parámetros:

 - **--defaultpath index.html**: indica que, a pesar de que posteriormente se acceda únicamente al directorio y no al fichero /index.html, este sea mostrado de manera predeterminada.
 - **--recursive**: necesario para subir de forma recursiva los ficheros y carpetas incluidos en el directorio indicado.
 - **--encrypt**: tal y como indica el enunciado, debe encriptarse la subida.

Así, la consola devuelve el siguiente hash:

    88ee6cf59ddf69059d38b8619a7bcd5f9abe7722d00633273f8cbc88b5acd64d4dd30221656bd764b05f297ea59a32517ace2aa99d5263f6fa83b84ef3251766

Y el nodo informa de la correcta subida:

    INFO [07-03|20:00:52.098] created ruid for request                 ruid=ba3ba5f3 method=POST url="/bzz:/encrypt?defaultpath=index.html"
    INFO [07-03|20:00:52.098] setting request host                     ruid=ba3ba5f3 host=127.0.0.1:8500
    INFO [07-03|20:00:52.316] request served                           ruid=ba3ba5f3 code=200 time=218.327345ms

Para acceder al directorio subido, basta con introducir este hash en la barra de búsqueda del localhost 8500 que puede observarse en la captura de pantalla anteriormente mostrada, o bien escribiendo directamente en la barra de direcciones la siguiente dirección:

> http://localhost:8500/bzz:/88ee6cf59ddf69059d38b8619a7bcd5f9abe7722d00633273f8cbc88b5acd64d4dd30221656bd764b05f297ea59a32517ace2aa99d5263f6fa83b84ef3251766

De esta forma, y tal y como se observa en la siguiente captura de pantalla, se accede a la web creada, concretamente al fichero index.html por defecto gracias al parámetro que se ha introducido:

![Swarm](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio3/Image2.png)

En la barra de direcciones de la siguiente imagen es posible observar cómo, efectivamente, el resultado es el mismo que si se accede diretamente al index.html:

![Swarm](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio3/Image3.png)

De igual forma, en las dos capturas de pantalla mostradas a continuación puede observarse cómo, tal y como se explicó anteriormente, el hash del Documento 1 y Documento 2 no cambia al acceder a cada uno de ellos:

![Swarm](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio3/Image4.png)

![Swarm](https://github.com/penalvaperez/DDI-PEC2/blob/master/DDI-PEC2-Ejercicio3/Image5.png)







