# Topología

## Campus

192.168.1.0

IT
192.168.2.0
50 usuarios

- server: 10

Marketing
192.168.3.0

## TODOs

Configurar DHCP

Configurar servidores

- Activacion de puertos
- Direcciones estáticas
- Intranet con direccion .10

Configurar router

- Configuracion de puertos
  - Ips
  - Activacion de puertos
- Guardar configuracion

Dispositivos
- Configurar DHCP

Wifi
- Configurar access point
  - SSID: 4geeks
  - Clave: 4geekswifi
  - Auth: WPA2-PSK
  - Configurar: laptop y smartphone

Intranet
- Activar servicio HTTP
- Activar y configurar DNS

access-list 100 deny tcp any host 192.168.2.10 eq www
access-list 100 deny tcp any host 192.168.2.10 eq 443
access-list 100 permit ip any any