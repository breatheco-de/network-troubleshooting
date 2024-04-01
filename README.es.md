# Solucionando problemas de red

<!-- hide -->
<a href="https://www.4geeksacademy.co"><img height="280" align="right" src="https://github.com/4GeeksAcademy/installing-windows-on-virtual-machine/blob/master/js-bg-badge.png"></a>

> By [@arnaldoperez](https://github.com/arnaldoperez) and [other contributors](https://github.com/4GeeksAcademy/installing-windows-on-virtual-machine/graphs/contributors) at [4Geeks Academy](https://4geeksacademy.co/)

![last commit](https://img.shields.io/github/last-commit/4geeksacademy/installing-windows-on-virtual-machine)
[![build by developers](https://img.shields.io/badge/build_by-Developers-blue)](https://4geeks.com)
[![build by developers](https://img.shields.io/twitter/follow/4geeksacademy?style=social&logo=twitter)](https://twitter.com/4geeksacademy)

*Estas instrucciones [están disponibles en 🇪🇸 español](https://github.com/4GeeksAcademy/installing-windows-on-virtual-machine/blob/main/README.es.md) :es:*
<!-- endhide -->

En este escenario simulas ser el responsable de la red de un campus de 4Geeks Academy. Deberás completar las configuraciones necesarias para poner en funcionamiento la red, e implementar medidas de seguridad para garantizar el uso correcto de los servicios internos.

Esta práctica abarca los siguientes temas:

1. Direcciones IP
2. Configuración de servicios DHCP
3. Configuración de DNS
4. Configuracion de redes WiFi
5. Listas de control de acceso (ACL)

<!-- hide -->
## Antes de empezar... algo relacionado con los tutoriales:

> Te necesitamos! Estos ejercicios están construidos y mantenidos por contribuciones de gente como tu. Si encuentras algún bug o error ortográfico, por favor reportalo.

## Instalación en un clic (recomendado)

Puedes empezar estos ejercicios en pocos segundos haciendo clic en: [Abrir en Codespaces](https://codespaces.new/?repo=4GeeksAcademy/python-beginner-programming-exercises) (recomendado) o [Abrir en Gitpod](https://gitpod.io#https://github.com/4GeeksAcademy/python-beginner-programming-exercises).

> Una vez ya tengas abierto VSCode, los ejercicios de LearnPack deberían empezar automáticamente, si esto no sucede puedes intentar empezar los ejercicios escribiendo este comando en tu terminal: `$ learnpack start`

## Instalación local:

1. Asegúrate de instalar [LearnPack](https://learnpack.co), node.js version 14+ y Python version 3+. Este es el comando para instalar LearnPack:

```bash
$ npm i @learnpack/learnpack@2.1.20 -g && learnpack plugins:install @learnpack/python@1.0.0
```

2. Clona o descarga este repositorio en tu ambiente local.

```bash
$ git clone https://github.com/4GeeksAcademy/python-beginner-programming-exercises.git
$ cd python-beginner-programming-exercises
```

> Nota: Una vez que termine de descargar, encontrarás la carpeta "exercises" que contiene todos los ejercicios.

3. Inicializa el tutorial ejecutando el siguiente comando al mismo nivel en el que se encuentra tu archivo learn.json: 

```bash
$ pip3 install pytest==6.2.5 pytest-testdox mock
$ learnpack start
```

<!-- endhide -->


## ¿Cómo están organizados los ejercicios?

Cada ejercicio es una pequeña aplicación de Python que contiene los siguientes archivos:

1. **app.py:** representa el archivo de entrada de Python que será ejecutado por el computador.
2. **README.es.md:** Contiene las instrucciones del ejercicio.
3. **test.py:** Contiene el script del test para el ejercicio (no es necesario que abras este archivo).

> Nota: Estos ejercicios tienen calificación automática. Los tests son muy rígidos y estrictos, mi recomendación es que no prestes demasiada atención a los tests y los uses solo como una sugerencia o podrías frustrarte.

## Colaboradores

Gracias a estas personas maravillosas ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)):

1. [Arnaldo Perez (arnaloperez)](https://github.com/arnaloperez) contribution: (build-tutorial) ✅, (documentation) 📖
  
2. [Alejandro Sanchez (alesanchezr)](https://github.com/alesanchezr),  contribution: (bug reports) 🐛

3. [Lorena Gubaira (lorenagubaira)](https://github.com/lorenagubaira), contribution: (bug reports) 🐛, contribution: (coder), (translation) 🌎

Este proyecto sigue la especificación [all-contributors](https://github.com/kentcdodds/all-contributors). ¡Todas las contribuciones son bienvenidas!

Este y otros ejercicios son usados para [aprender a programar](https://4geeksacademy.com/es/aprender-a-programar/aprender-a-programar-desde-cero) por parte de los alumnos de 4Geeks Academy [Coding Bootcamp](https://4geeksacademy.com/us/coding-bootcamp) realizado por [Alejandro Sánchez](https://twitter.com/alesanchezr) y muchos otros contribuyentes. Conoce más sobre nuestros [Cursos de Programación](https://4geeksacademy.com/es/curso-de-programacion-desde-cero?lang=es) para convertirte en [Full Stack Developer](https://4geeksacademy.com/es/coding-bootcamps/desarrollador-full-stack/?lang=es), o nuestro [Data Science Bootcamp](https://4geeksacademy.com/es/coding-bootcamps/curso-datascience-machine-learning).