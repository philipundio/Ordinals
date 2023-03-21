# Ordinals
Creación de un nodo de Bitcoin e instalación de cartera Ord para inscribir de manera local en Windows.

En primer lugar nos debemos descargar la versión de Bitcoin Core 24.0.1 ya que es ésta la que interactúa con la waller Ord.
El enlace para proceder con la descarga es el siguiente. https://bitcoincore.org/en/download/

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

Aquí terminaríamos con éxito la tarea de tener un nodo totalmente sincronizado con la red.

El siguiente paso que debemos hacer es indexar los bloques de la cadena. Todos esos bloques estarán ya en nuestro ordenador en la carpeta que hayamos elegido para guardar nuestro nodo, por tanto vamos a ver cómo hacerlo.

    1. Iremos a nuestra carpeta donde tengamos instalado Bitcoin Core y dentro de ella cliquearemos en la carpeta llamada "daemon" (es posible que también se llame bin). Una vez dentro buscaremos el archivo "bitcoind" y haciendo click derecho seleccionaremos "Crear acceso directo" y pondremos este icono donde más conveniente sea. Os recomendamos el escritorio.
    
    2. Una vez nuestro acceso directo está creado, haremos click derecho sobre él y pincharemos en propiedades donde nos aparecerá la siguiente ventana.
    
    ![image](https://user-images.githubusercontent.com/114155448/226595198-db58c94e-8480-4b39-834e-fe94eca6ba94.png)

    En destino pondremos lo siguiente: **D:\Bitcoin24\daemon\bitcoind.exe -datadir=D:\Bitcoin24 -txindex=1**
