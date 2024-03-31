### 💡Laboratorio:

**Descripción del Escenario:**

Eres un consultor de redes y te han contratado para mejorar la arquitectura de red de una pequeña empresa. La empresa actualmente tiene una red que ha crecido orgánicamente con el tiempo y está experimentando problemas de rendimiento y seguridad. Tu tarea es evaluar la situación actual y proponer mejoras. Cuentas con la siguiente información:

1. Se trata de una red LAN de 10 equipos y 1 servidor web
2. Los usuarios manifiestan que la red es lenta y no hay una topología precisa establecida
3. Los dispositivos de red son obsoletos
4. Todos los equipos tienen acceso a internet y también a la intranet de la empresa, esta última  a través del servidor web de la red local

**Preguntas y Desafíos:**

1. **Evaluación de la Situación Actual:**
    - ¿Cuál es el alcance de la red actual? ¿Cuántos dispositivos y usuarios están conectados?
    - ¿Qué problemas específicos de rendimiento o seguridad ha experimentado la empresa?
2. **Topología de Red:**
    - ¿Qué topología de red utilizarías  para esta empresa?
    - ¿Cómo se deben conectar los dispositivos y los servidores?
3. **Equipos de Red:**
    - ¿Qué tipo de dispositivos de red se necesitan? (routers, switches, firewalls, etc.)
    - ¿Qué especificaciones técnicas deben cumplir estos dispositivos?
4. **Seguridad de la Red:**
    - ¿Cuáles son las medidas de seguridad necesarias para proteger la red?
    - ¿Cómo se deben configurar los dispositivos de seguridad, como el firewall?
5. **Gestión de la Red:**
    - ¿Cómo se gestionarán y supervisarán los dispositivos de red?
    - ¿Se implementará un sistema de gestión de red (NMS) o herramientas de monitorizaciónn?
6. **Plan de Implementación:**
    - ¿Cuál es el cronograma de implementación de las mejoras propuestas?
    - ¿Cómo se comunicarán estos cambios a los empleados?
7. **Mantenimiento Continuo:**
    - ¿Qué medidas se tomarán para garantizar el mantenimiento y la actualización continua de la red?
    - ¿Se establecerán políticas de seguridad y procedimientos de respuesta a incidentes?
8. **Evaluación del Éxito:**
    - ¿Cómo se medirá el éxito de las mejoras? ¿Qué métricas se utilizarán para evaluar el rendimiento y la seguridad de la red después de la implementación?

> ⚠️ **Recuerda: No hay respuestas incorrectas en cuanto a topologías de red y dispositivos, intenta hacer la red lo más óptima posible.**

### 💡Laboratorio: Diseña una red LAN

Con todo lo anterior mencionado descarga el software gratuito de Cisco llamado Cisco Packet Tracer y resuelve el siguiente desafío:

Eres un administrador de red contratado por 4Geeks Academy y en tu primer día de trabajo, el jefe de seguridad y comunicaciones te asigna el diseño de una red LAN que conecta a los 8 computadores que conforman la red del departamento de educación y entregar un presupuesto estimado sobre el costo total de la instalación de la red. Para resolver este desafío deberás:

1. Descargar el software gratuito de Cisco: Cisco Packet Tracer, con este programa podrás diseñar una red LAN de forma visual
2. Investigar sobre precios y características de los dispositivos de red que necesitarás para diseñar tu red LAN y elaborar un presupuesto
3. Elabora un informe técnico en el que expliques el diseño de la red LAN 

> 💡Pistas: Elige la topología de red que estimes conveniente (No hay respuestas incorrectas), recuerda que no es necesario utilizar todos los dispositivos de red vistos durante tu aprendizaje y que a veces menos es más. En tu informe técnico, explica tus decisiones y porqué es la forma más óptima de crear una red LAN.

### 💡Laboratorio: Configuración de Firewall

En el siguiente laboratorio vamos a aprender a configurar un firewall con la ayuda de cisco packet tracer, siguiendo los siguientes pasos

1. Abrimos Cisco Packet Tracer y creamos un entorno simulado con: Dos computadoras conectadas a un Switch, el Switch estará conectado un router y el router a un servidor web como en la siguiente imagen:

![Configuración de Firewall](https://github.com/4GeeksAcademy/cybersecurity-syllabus/blob/main/assets/confirguracion-firewall.png?raw=true)

2. Configuramos PC0 Y PC0 con ip estáticas, haciendo click en cada una e ingresando en la pestaña Desktop

IP Address 192.168.1.2 / 192.168.1.3

Subnet Mask 255.255.255.0

Default gateway 192.168.1.10

Podemos hacer ping a cada ip para verificar que la conexión entre ambas PC esté establecida

3. Configuramos la IP del servidor

IP Address 200.200.200.200

Subnet Mask 255.255.255.0

Default gateway 200.200.200.201

4. Configurarmos el router en las opciones de FastEthernet0/0 y FastEthernet0/1.

La dirección IP serán los Default Gateway de los dispositivos

ip address 192.168.1.10 (Para FastEthernet0/0) 200.200.200.201 (Para FastEthernet0/1)

5. Emitimos un ping desde las computadoras clientes al servidor web haciendo un ping 200.200.200.200 para confirmar que hay conexion entre ambos dispositivos.

6. Entramos de nuevo al router y nos dirigimos a la pestaña cli donde ingresamos los siguientes comandos

![Pestaña Cli](https://github.com/4GeeksAcademy/cybersecurity-syllabus/blob/main/assets/pestana-cli.png?raw=true)

1. Hacemos ping de nuevo al servidor desde las computadoras clientes, se perderán todos los paquetes enviados ya que desde el router con los comandos anteriores programamos para que el protocolo ICMP quedará deshabilitado y solo se permitirá a los clientes acceder al servicio web
2. Por último desde cualquier computadora cliente accederemos al servicio web, ingresando a la opcion web browser e ingresando 200.200.200.200 en el buscador. nos mostrará una página llamada index.html