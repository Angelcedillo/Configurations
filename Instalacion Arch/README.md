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

La primera opcion es por cable, la coneccion por cable de red directamente desde tu router es la mas sencilla, ya que solo conectas el cable y en automatico tienes internet en la PC.

La segunda opcion es por WI-FI, en esta tenemos que hacer un par de comandos para configurar el internet.

Los comandos son los siguientes:

```bash
wpa_passphrase "nombre de tu red sin comillas" "contraseña de tu red sin comillas" > /etc/wifi 
```
```bash
wpa_supplicant -B -i wlan0 -D wext -c /etc/wifi
```
Al momento de realizar los comandos anteriores saldran unos mensajes de error, pero no pasa nada, la coneccion ya esta lista, lo podemos verificar con un Ping a cualquier pagina.

```bash
ping 8.8.8.8
```
Si el ping manda respuesta de coneccion con la pagina, Felicidades ya tienes coneccion a internet y podemos seguir con la instalacion.
