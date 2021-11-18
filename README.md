# IBM Cloud ☁ - Despliegue de aplicación Angular-Web-List en Kubernetes <img width="30" src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/kubernetes.png">

## Índice  📰
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Crear clúster Kubernetes](#Crear-clúster-Kubernetes-cloud)
3. [Instalar herramientas y comandos necesarios](#Instalar-herramientas-y-comandos-necesarios-gear)
4. [Clonar repositorio](#Clonar-repositorio-round_pushpin)
5. [Crear imagen docker local de la aplicación](#Crear-imagen-docker-local-de-la-aplicación-computer)
6. [Desplegar aplicación en Kubernetes](#Desplegar-aplicación-en-Kubernetes-rocket)
7. [Verificar el funcionamiento de la aplicación](#Verificar-el-funcionamiento-de-la-aplicación-heavy_check_mark)
8. [Referencias](#Referencias-mag)
9. [Autores](#Autores-black_nib)
<br />

## Pre-Requisitos :pencil:
* Tener una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a> <img width="25" src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/ibm-cloud-logo.png">.
<br />

## Crear clúster Kubernetes :cloud:
Para crear un clúster de Kubernetes y desplegar la aplicación propuesta en el presente repositorio, complete los siguientes pasos:
<br />

1. Inicie sesión con su usuario y contraseña en el portal de <a href="https://cloud.ibm.com/"> IBM Cloud</a>.

2. Una vez se encuentre en el dashboard del portal, de click en el menú de navegación o hamburguesa que se encuentra en la parte superior izquierda (lo puede identificar mediante 4 líneas blancas) y allí seleccione la pestaña ```Kubernetes```.

3. Espere unos segundos mientras carga la ventana y luego de click en el botón ```Create cluster +/Crear cluster +```.

4. Complete los detalles del plan de la siguiente manera:

   * ```Princing plan/Plan de precios```: seleccione la opción **Free**.
   * ```Cluster name/Nombre del clúster```: indique un nombre exclusivo para su clúster.
   * ```Resource group/Grupo de recursos```: seleccione el grupo de recursos **Default** que aparece por defecto.

5. Para finalizar la creación de su clúster de click en el botón ```Create/Crear```. Cuando el clúster tengo como estado ```normal```, podrá utilizarlo.

   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/CrearCluster.gif"></p>

   <br />

> NOTA: Después de dar click en el botón crear, el proceso de despliegue del clúster puede tomar entre 20 y 30 minutos. Por lo tanto, se recomiendo continuar con la siguiente sección sobre como [Instalar herramientas y comandos necesarios](#Instalar-herramientas-y-comandos-necesarios-gear), mientras se completa la creación del clúster.

<br />

## Instalar herramientas y comandos necesarios :gear:
Para desplegar la aplicación propuesta en un clúster de Kubernetes en IBM Cloud, deberá contar con una serie de comandos y herramientas que le permitirán completar el proceso con éxito. A continuación, se indican los pasos para realizar la instalación en Windows. En caso de que trabaje con un sistema operativo diferente, se indican los enlaces para que revise el proceso.
<br />

### Instalación de git
Teniendo en cuenta que debe clonar el presente repositorio para usar la aplicación, es necesario contar con el comando git. Complete los siguientes pasos para realizar realizar la instalación:
<br />

1. Verifique si tiene instalado el comando. Para ello, abra una ventana de ```Windows PowerShell``` y allí coloque:

   ```PowerShell
   git --version   
   ```
   
   Si obtiene como respuesta la versión de git, puede pasar a la siguiente sección sobre la [Instalación de Docker](#Instalación-de-Docker). De lo contrario, continúe con el paso 2.

2. Para instalar git en su computador, vaya a la página de <a href="https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Instalaci%C3%B3n-de-Git"> Instalación de Git</a>. Identifique el sistema operativo en el que desea realizar la instalación y complete el proceso indicado. Para el caso de Windows, de click sobre el enlace <a href="http://git-scm.com/download/win"> http://git-scm.com/download/win</a>, y allí seleccione la opción ```Click here to download manually```. 

3. Espere mientras se completa la descarga y posteriormente, de click en el instalador. Complete la instalación, dejando todos los campos como aparecen por defecto y al final de click en el botón ```Install```.

4. Para verificar que la instalación de git se ha completado con éxito, en una ventana de ```Windows PowerShell``` coloque:

   ```PowerShell
   git --version   
   ```
   
   Como respuesta debe obtener la versión de git.
   
   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/Instalar%20Git.gif"></p>

   <br />

## Instalación de Docker
Para crear la imágen docker local de la aplicación y probarla, es necesario que instale *Docker Desktop*. Para ello, complete los siguientes pasos:
<br />

1. Vaya a la página <a href="https://docs.docker.com/desktop/"> Docker Desktop overview</a> y seleccione las pestaña segpun su sistema operativo. Para el caso de Windows, de click en la sección ```Install Docker Desktop on Windows``` y luego presione el botón ```Docker Desktop for Windows```.

2. Espere unos minutos mientras se completa la descarga, y luego de click sobre el instalador.

3. Habilite la 2 casillas que aparecen y de click en el botón ```Ok```. Espere unos minutos mientras se completa la instalación.

4. Una vez finalice la instalación, en la barra de búsqueda coloque ```Docker Desktop``` y abra la aplicación. Espere unos minutos mientras esta inicia.

5. Si no tiene una cuenta en <a href="https://hub.docker.com/"> DockerHub</a>, cree una y luego coloque las credenciales de inicio de sesión presionando ```Sign in``` en la parte superior derecha de la ventana de ```Docker Desktop```.

   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/Instalar%20Docker.gif"></p>
  
   <br />
   
   > NOTA: En caso de presentar problema en Windows sobre *Enable Hyper-V Windows Features*, revise la guía <a href="https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v"> Enable Hyper-V using PowerShell</a>
  
6. Una vez complete la instalación, en un ventana de ```Windows PowerShell``` coloque:

   ```PowerShell
   docker version   
   ```
   
   Como respuesta debe obtener la versión de docker.
   
   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/Prueba%20Docker.gif"></p>

   <br />
   
### Instalar IBM Cloud CLI y plug-ins
<br />

## Clonar repositorio :round_pushpin:
<br />

## Crear imagen docker local de la aplicación :computer:
<br />

## Desplegar aplicación en Kubernetes :rocket:
<br />

## Verificar el funcionamiento de la aplicación :heavy_check_mark:
<br />

## Referencias :mag:
<br />

## Autores :black_nib:
Equipo *IBM Cloud Tech Sales Colombia*.
