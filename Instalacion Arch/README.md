# Instalacion de ArchLinux (BIOS).

Una vez estando en la linea de comandos de el instalador de ArchLinux empezaremos a instalar el Sistema Operativo ArchLinux.

# Configurar Teclado.

Lo  primero es cargar la distribucion de teclado que mas se acomode. Para ello ocupamos el siguiente comando.

```bash
loadkeys la-latin1
```
Donde "la-latin1" es la distribucion Latinoamericana, esta se cambia a la distribucion que ocupes tu.

# Conectar internet.

Aqui hay dos maneras de conectarse a internet.

La primera opcion es por cable, la conexion por cable de red directamente desde tu router es la mas sencilla, ya que solo conectas el cable y en automatico tienes internet en la PC.

La segunda opcion es por WI-FI, en esta tenemos que hacer un par de comandos para configurar el internet.

Los comandos son los siguientes:

**para wifi sin seguridad**
```bash
iwconfig wlan0 essid "nombre de tu red sin comillas"
```

**para wifi con seguridad wpe**
```bash
iwconfig wlan0 essid "nombre de tu red sinn comillas" key s:"contraseña de tu red sin comillas"
```

**para wifi con seguridad wpa/wpa2**
```bash
wpa_passphrase "nombre de tu red sin comillas" "contraseña de tu red sin comillas" > /etc/wifi 
wpa_supplicant -B -i wlan0 -D wext -c /etc/wifi
```
Al momento de realizar los comandos anteriores saldran unos mensajes de error, pero no pasa nada, la conexion ya esta lista, lo podemos verificar con un Ping a cualquier pagina.

```bash
ping 8.8.8.8
```
Si el ping manda respuesta de conexion con la pagina, Felicidades ya tienes conexion a internet y podemos seguir con la instalacion.

# Particionar Disco.

En este apartado cada Usuario puede particionar diferente el disco, pero yo suelo ocupar esta particion en todas mis instalaciones de ArchLinux.

![InstalacionArch](../images/Particion.jpeg)

Sin tomar en cuenta las particiones de: **boot windows y disco c:** te explicare como particionar el espacio que necesita ArchLinux. 

ocuparemos la particion de intercambio (opcional), mejor conocida como **SWAP**, y la particion de montaje donde vendran las particiones de **Boot, Home y Root**.

Para comenzar a particionar el disco ocuparemis una herramienta de terminal llamada **cfdisk**. Ocuparemos el siguiente comando:

```bash
cfdisk /dev/sda
```

Normalmente **/dev/sda** es el disco por defecto de la computadora.

Una vez abierto cfdisk haremos las siguientes particiones: **(cada particion depende del tamaño de disco y si es un solo Sistema operativo o mas)**

en cfdisk seleccionaremos un espacio libre selecciona para ArchLinux, y daremos click en la opcion Nuevo.

![Cfdisk](../images/Cfdisk.jpg)

Esta particion la asignaremos como primaria y le asignaremos 2GB. de espacio.

Despues seleccionaremos esa misma particion y seleccioanremos ahora la opcion de **Tipo** y seleccionaremos **swap**.

Ahora seleccionaremos el espacio libre disponible y volveremos a dar en nuevo, Esta vez a esta particion la dejaremos con el espacio restante, para ello damos un enter.

Listo, a esta particion no hay que cambiarle el tipo de particion, ya que por defecto la marca con el tipo que necesitamos, en este caso, **Linux**.

Solo nos queda dar enter en la opcion **Escribir** y las particiones se habran guardado correctamente.

![Cfdisk](../images/IMG_20201116_190948.jpg)

Listo, Asi es como nos deberian de quedar nuestras particiones.

Lo siguiente que tenemos que hacer es formatear las particiones que hemos creado, para esto hacemos lo siguiente:

**Primero para la particion de SWAP**
```bash
mkswap /dev/sdaX
swapon /dev/sdaX
```
Donde X se cambia por la particion donde se creo swap.

**Para la segunda particion**
```bash
mkfs.ext4 /dev/sdaX
```
Donde X se cambia por la particion donde se creo.

# Montar las particiones.
