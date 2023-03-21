# Ordinals
Creación de un nodo de Bitcoin e instalación de cartera Ord para inscribir de manera local en Windows.


>**En primer lugar nos debemos descargar la versión de Bitcoin Core 24.0.1 ya que es ésta la que interactúa con la waller Ord.
El enlace para proceder con la descarga es el siguiente. https://bitcoincore.org/en/download/**

Una vez descargado el archivo zip, hay que descomprimirlo en la carpeta donde se quiere tener el programa instalado. **Se recomienda fervientemente que la carpeta que se elija para la instalación de Bitcoin Core esté en un disco SSD si fuese posible. El tamaño de disco necesario será de 1TB para ir seguros.**

Dentro de la carpeta tendremos que buscar el archivo ejecutable "Bitcoin-qt" que abrira nuestro Bitcoin Core.

Una vez éste sea instalado, podemos ejecutar Bitcoin Core directamente, es muy importante que la configuración sea la siguiente en la primera ventana que veremos:
  - Utilizaremos un directorio personalizado como destino para nuestro nodo, por ejemplo: D:\Bitcoin24
  
  - La última línea de la ventana que tendremos abierta dice así "Limitar el almacenamiento de la cadena de bloque a...". Debemos NO hacer tick en la casilla, pues lo que buscamos es tener la cadena de bloques completa en nuestro ordenador.

![image](https://user-images.githubusercontent.com/114155448/226586134-9a6c51e0-42a4-44e3-9334-ce785caa2570.png)

  - Pulsamos OK y normalmente saltará el firewall de Windows. Hemos de permitir acceso.

Bitcoin core en estos momentos empezará a descargar todos los bloques de la cadena Bitcoin desde su creación. Este paso puede tomar fácilmente 1 día, dependerá principalmente de dos factores: nuestra conexión a internet y la capacidad de "write" que tenga el disco duro donde estemos descargando el nodo. Se puede seguir utilizando el ordenador sin problema y dejando este proceso en segundo plano minimizado.

Una vez nuestro nodo está completamente sincronizado con la red, la ventana de Bitcoin Core lucirá como en la siguiente imagen:

![image](https://user-images.githubusercontent.com/114155448/226587838-1f3e4191-a378-4829-9a26-f48a95507b61.png)

Aquí terminaríamos con éxito la tarea de tener un nodo totalmente sincronizado con la red. Procedemos a cerrar la aplicación.


>**El siguiente paso que debemos hacer es indexar los bloques de la cadena. Todos esos bloques estarán ya en nuestro ordenador en la carpeta que hayamos elegido para guardar nuestro nodo, por tanto vamos a ver cómo hacerlo.**

1. Iremos a nuestra carpeta donde tengamos instalado Bitcoin Core y dentro de ella cliquearemos en la carpeta llamada "daemon" (es posible que también se llame bin). Una vez dentro buscaremos el archivo "bitcoind" y haciendo click derecho seleccionaremos "Crear acceso directo" y pondremos este icono donde más conveniente sea. Os recomendamos el escritorio.
    
2. Una vez nuestro acceso directo está creado, haremos click derecho sobre él y pincharemos en propiedades donde nos aparecerá la siguiente ventana.
    
    ![image](https://user-images.githubusercontent.com/114155448/226595198-db58c94e-8480-4b39-834e-fe94eca6ba94.png)

    En destino pondremos lo siguiente: **D:\Bitcoin24\daemon\bitcoind.exe -datadir=D:\Bitcoin24 -txindex=1**. El primer comando "-datadir=D:\Bitcoin24" Será la carpeta donde tengamos instalado nuestro nodo, en nuestro caso D:\Bitcoin24. El segundo comando a añadir "-txindex=1" es el comando que le dice a bitcoind que debe indexar los bloques una vez ejecutemos éste.
    
    Este paso es necesario ya que bitcoind sin estos matices que acabamos de añadir, volvería a descargar por completo la cadena de bloques y de este modo, le estamos mostrando dónde está descargada y pidiendo que la "indexe". Durante todo este proceso Bitcoin Core ha de permanecer cerrado.
    
3. Abriremos el programa "bitcoind" desde nuestro acceso directo. Ahora mismo el programa está indexando todos los bloques contenidos en nuestro disco duro. Esta tarea puede tardar mucho tiempo, incluso más que la descarga del nodo. El programa ha de lucir como la siguiente imagen:

![image](https://user-images.githubusercontent.com/114155448/226599344-17cca59b-daf5-4322-9a4c-296060fe011e.png)

   En las líneas de código que vemos la parte más importante es "height" pues define el número de bloque por el que vamos. Podemos chequear cuánto nos queda para llegar a una indexación total comparando con la mempool actual aquí: https://mempool.space/
   
Cuando veamos que nuestro height es el mismo que el que encontramos en la mempool, lo vamos a corroborar a través de nuestro nodo de la siguiente manera (importante: bitcoind debe permanecer abierto):

- Nos dirigimos de nuestro a nuestra carpeta donde tenemos instalado el nodo, y entraremos en la carpeta "daemon" o "bin". Una vez dentro, la ejecutaremos desde el cmd de windows, y en el terminal escribiremos lo siguiente: "bitcoin-cli getblockcount" donde obtendremos algo como esto:

![image](https://user-images.githubusercontent.com/114155448/226605774-91850a6f-a396-48f8-9188-aa2c8af36bd1.png)
  
  Es posible, que nos devuelva un error de RPC cookie, si este fuera el caso, nos iremos a nuestra carpeta del nodo y bucaremos el archivo ".cookie", y haciendo click derecho seleccionaremos "copiar como ruta de acceso". Posteriormente volveremos a nuestro cmd donde obtuvimos este error y escribiremos lo siguiente: "bitcoin-cli -rpccookiefile=(aquí haremos crtl+V) getblockcount". Esto nos devolvería el bloque hasta el que hemos indexado, que una vez más ha de coincidir con el mempool. Debería lucir así:
  
  ![image](https://user-images.githubusercontent.com/114155448/226607028-5ea9129d-6bfd-458c-94f0-df28d8d231d9.png)

Una vez hecho esto, tendremos nuestro nodo completamente indexado. Bravo!!

>**Instalación Ord Wallet**

Una vez tenemos nuestro nodo sincronizado e indexado, nos queda descargarnos e instalar nuestra Ord Wallet.
Lo haremos directamente desde el sitio oficial de Ordinals en el siguiente enlace https://github.com/casey/ord/releases/tag/0.5.1. En el apartado de assets seleccionaremos el siguiente archivo "ord-0.5.1-x86_64-pc-windows-msvc.zip".
Recomendamos extraer ord wallet dentro de la carpeta de Bitcoin Core y nombrarla ORD, por razones prácticas.

Una vez extraída en la carpeta de destino, la abriremos a través del cmd. Lo que nos dará algo como esto (importante, debemos tener bitcoind abierto):

![image](https://user-images.githubusercontent.com/114155448/226613306-7cee6848-8cb6-476e-a45a-fdd2b93f0e4a.png)

El primer paso será crear una cartera con el siguiente comando: ord wallet create
Es posible que volvamos a tener un problema de RPC, lo que solucionaremos del mismo modo que antes, con nuestro archivo .cookie. Por lo tanto nuestra línea de código debe ser "ord --cookie-file (ctrl+V) wallet create"
Cuando el paso sea exitoso, recibiremos una clave pnemotécnica que deberemos guardar para un posible recovery futuro.

Ahora vamos a indexar los bloques desde ord wallet. Este paso es necesario ya que ord wallet hace un tracking de cada satoshi contenido en la cadena de bloques, pues son éstos los que llevarán inscritos nuestros Ordinals. Para ello, en la consola escribiremos: "ord wallet balance". Este paso lleva de nuevo bastantes horas, por lo que recomendamos dejarlo correr en segundo plano mientras hace la indexación. Lucirá como sigue:

![image](https://user-images.githubusercontent.com/114155448/226623905-c8a57478-32da-45ed-9d47-77c7c53ca834.png)

Una vez los bloques han sido indexados, recibiremos la respuesta del balance que debería ser "D:\Bitcoin24\ord>ord wallet balance

{
  "cardinal": 0
}"

Esto es lógico pues no hemos enviado aún fondos a nuestra cartera. Para ello, utilizaremos el siguiente comando: "ord wallet receive". Esto nos devolverá una dirección de cartera que comenzará por bc1p, característica de las direcciones de Taproot.






   
    
