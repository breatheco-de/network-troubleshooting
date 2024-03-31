# Instrucciones

## 1. Introducción

En esta ocasión te presentamos lo que podría ser la red de 4Geeks Academy en una de nuestras sedes. Es un escenario que se suele ver en muchos entornos empresariales.

Contamos con un router que representa la conexión entre varias redes de la misma empresa. En este caso corresponden a 3 áreas distintas, el campus de estudiantes, el departamento de marketing y el departamento de IT.

Como puedes ver todas las redes cuentan con direcciones privadas clase C que puedes ver en las notas en su respectiva área coloreada.

Para esta práctica debemos realizar lo siguiente:

- Configurar el servidor DHCP de cada red para que los equipos puedan obtener direcciones IP de forma dinámica
- Configurar los enlaces entre dispositivos.
- Configurar la red WiFi del campus
- Configurar el servidor de Intranet
- Configurar lista de acceso para restringir el acceso a la Intranet desde el campus

Avanza a la siguiente página para comenzar.

## 2. Direcciones IP

Como puedes observar en cada área coloreada están anotadas las direcciones de IP de las redes, y cada una tiene una mascara `/24` que también puede ser expresada como `255.255.255.0`, lo que significa que de cada red puedes asignar direcciones desde la 1 hasta la 254, por ejemplo:

```text
192.168.0.0 - Dirección de red
192.168.0.1 - Primera dirección asignable
192.168.0.254 - Última dirección asignable
192.168.0.255 - Dirección de difusión o broadcast
```

**En base a esto configura lo siguiente:**

- Asigna la primera dirección de la red a la puerta de enlace en el router, según la interfaz que corresponda.
- Configura direcciones ip estática en los servidores, utilizando las anotaciones en cada red.
- Todas las interfaces deben estar activadas para que haya conectividad.

Recuerda que para el caso del router debes verificar que todas las interfaces estén encendidas, asi como también guardar la configuración en la NVRAM para que los cambios persistan después de un reinicio.

Al terminar este paso deberás tener conectividad entre los servidores y el router.

## 3. Servidores DHCP

Una vez establecida la conexión entre los servidores y el resto de la red, es hora de que los utilices para asignar direcciones a los demás dispositivos.

En cada uno de ellos debes configurar una piscina o pool de direcciones que serán utilizadas para asignarlas a los equipos que se vayan conectando a la red. Los valores que conforman cada pool son los siguientes:

- **Default Gateway:** Dirección ip del router, es decir la primera dirección de la red (Ejemplo 192.168.0.1)
- **DNS Server:** Es el servidor de nombres de dominio, en este caso utiliza `192.168.2.10` que corresponde al servidor de la intranet que presta este servicio.
- **Start Ip Address:** Corresponde a la dirección desde la cual empezarán a asignarse las direcciones IP. En este caso empieza desde la dirección 100 de la red (Ejemplo: 192.168.2.100)
- **Subnet Mask:** Es la mascara de subred que en este caso es `255.255.255.0`
- **Maximum number of users:** El máximo numero de usuarios debe ser `100`

Una vez que hayas establecido estos valores, debes presionar el botón `Save` para guardar los cambios del pool. El resto de los valores se quedan por defecto.

En la opción `Settings` de la pestaña `Config` debes configurar de forma estática la puerta de enlace (Default gateway) y el DNS. Recuerda que la puerta de enlace de cada red es la primera dirección asignable del rango de direcciones ip de nuestra red, mientras que para el DNS apunta al servidor Intranet: 192.168.2.10

Recuerda variar las direcciones de red correspondiente para cada servidor. Cuando los hayas configurado todos, es turno de que actives la opción DHCP en cada dispositivo final para que adquieran conectividad.

## 4. Red WiFi

Como parte de la red del campus tenemos un punto de acceso inalámbrico que debe ser configurado. Este dispositivo va a extender nuestra red via WiFi, incorporando los dispositivos inalámbricos como si fueran parte de la red cableada y de manera segura usando una clave de acceso.

En el puerto inalámbrico del `AccessPoint` debes configurar lo siguiente:

- **SSID:** 4geeks
- **Authentication:** WPA2-PSK
- **PSK Pass Phrase:** 4geekswifi
- **Encryption type:** AES

Estos son los parámetros básicos que se deben configurar para tener acceso inalámbrico. Luego de ello debes configurar los mismos parámetros en los dispositivos inalámbricos (Laptop y Smartphone) en sus respectivas interfaces `Wireless` para que estos se conecten a la red.

## 5. Servidor de Intranet

Este servidor representa los servicios internos que se usan en la red de 4geeks. En este caso presta servicios de DNS y Web, los cuales se configuran en la pestaña `Services`.

El servidor web ya esta cargado con la página que debe mostrar y solo necesitas activarlo con ambos protocolos, HTTP y HTTPS.

El servicio DNS debe ser activado y se le agregará un registro para que dirija la dirección `4geeks.com` hacia la intranet. Debes configurar lo siguiente:

- **Name:** 4geeks.com
- **Type:** A Record
- **Address:** 192.168.2.10

Presiona el botón `Add` para crear el registro. Si seguiste correctamente las anotaciones en el paso 3, el servidor Intranet debe tener configurada la ip `192.168.2.10` de forma estática. Ya con esto, si accedes al navegador desde el escritorio de alguna de las pc de la red, puedes ver la página `4geeks.com`

## 6. Lista de acceso

Todo bien hasta ahora, pero tenemos una falla de seguridad. Nuestra intranet está expuesta a las personas que llegan al campus y esto compromete la integridad de nuestra información. Debes impedir que se acceda a la intranet desde el campus, pero sin afectar el servicio de DNS que es vital para el funcionamiento normal de la red, ni tampoco bloquear el acceso desde los demás departamentos de 4geeks que necesitan acceso a la intranet.

Esto lo logras con una lista de acceso, las cuales son reglas que utilizará el Router para determinar si permite o no el paso de cierta información que va llegando por sus interfaces.

En este caso se deben configurar 3 reglas para la interfaz de la red del campus:

1. Negar el paso a paquetes que se dirijan al servidor usando el puerto 80
2. Negar el paso a paquetes que se dirijan al servidor usando el puerto 443
3. Permitir el resto de las conexiones

Para ello nos adentraremos en la interfaz de linea de comando del router en la pestaña `CLI` donde debes ejecutar los siguientes comandos

1. `enable` *Activa la interfaz con privilegios*

2. `config terminal` *Entra en modo de configuración*

3. `interface gigabit 0/0` *Entra en la configuración de la interfaz de la red del campus*

4. `ip access-group 100 in` *Agrega la interfaz dentro del grupo de la lista de acceso '100'*
5. `exit` *Sale de la configuración de la interfaz*

6. `access-list 100 deny tcp any host 192.168.2.10 eq www` *Agregar una regla a la lista de acceso '100' para no permitir paquetes hacia el servidor de intranet que usen el puerto 80*

7. `access-list 100 deny tcp any host 192.168.2.10 eq 443` *Agregar una regla a la lista de acceso '100' para no permitir paquetes hacia el servidor de intranet que usen el puerto 443*

8. `access-list 100 permit ip any any` *Regla para permitir el resto del tráfico en la red. Debe especificarse de última*

9. `do write` *Guarda la configuración en la NVRAM*

Puedes verificar el funcionamiento de esta lista de acceso intentando acceder a 4geeks.com desde una PC del campus, lo cual te debería retornar un error `Requested timeout`, aunque una prueba de ping si debe funcionar correctamente.

