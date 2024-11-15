# Oracle OKIT
Instalacion y Configuracion de OKIT

## Que es OKIT ?

Es un kit de herramientas de diseño y visualización, adicionalmente es una herramienta basada en navegador que permite al usuario diseñar, implementar y visualizar (introspeccionar/consultar) entornos OCI a través de una interfaz gráfica basada en web.

### Pasos para la instalación

1. Creacion de la VCN en OCI:
   #### Menú>Networking>Virtual Cloud Networks
   Seleccionamos Start VCN Wizard y seguimos el flujo de creacion asignando el nombre, el rango de CIDR, subnets etc.
     
   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/Start-Wizard.jpg)


   1.1 Crear Internet Gateway
   #### Menú>Networking>Virtual Cloud Networks>Internet Gateways

   #### Asignar nombre y crear

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/IGW-create.jpg)
   
   1.2 Configurar la Tabla de Rutas y Security List de la Subred
   #### Menú>Networking>Virtual Cloud Networks>Route Tables

   #### Asignar nombre a la tabla y adicionar las rutas necesarias, en este caso vamos a adicionar la rutas para conectividad desde y hacia Internet seleccionando el Internet Gatewat creado en el paso anterior

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/RT-create.jpg)

   #### Security List
   #### Menú>Networking>Virtual Cloud Networks>Security Lists
   #### Crear las entradas de Ingress y Egress en la SL

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/SL-create.jpg)

2. Creacion de Virtual Machine en OCI
   #### Menú>Compute>Instances>Create Instance

   #### Completar informacion de AD, Shape, Imagen, Red y cargar llave SSH

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/VM-create.jpg)


3. Actualizacion del Sistema Operativo
   #### Conectarse a la VM por SSH y enviar el comando: sudo dnf update -y

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/DNF-update.jpg)

4. Instalacion y configuracion del motor y el cliente de Docker

   4.1 Instalar el repositorio de descarga de la version CE de Docker
   
   #### Conectarse a la VM por SSH y ejecutar los siguientes comandos:

   #### sudo dnf install -y dnf-utils zip unzip
   #### sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
   #### sudo dnf install docker-ce docker-ce-cli containerd.io

   4.2 Iniciar el servicio y configurar Docker para inicio con el Sistema Operativo

   #### Conectarse a la VM por SSH y ejecutar los siguientes comandos:

   #### sudo systemctl start docker
   #### sudo systemctl enable docker
   #### sudo systemctl status docker

   El servicio debe estar en el siguiente estado

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/Docker-status.jpg)

   4.3 Configurar usuario OPC para ejecucion de comandos docker:

   #### Conectarse a la VM por SSH y ejecutar los siguientes comandos:
   #### sudo usermod -aG docker opc
   #### Hacer logout y login para que el usuario tome los cambios

6. Instalacion y Configuracion de OCI CLI

   5.1 Para la instalacion de la linea de comando de OCI debemos seguir los siguientes pasos:

   #### Conectarse a la VM por SSH y ejecutar los siguientes comandos:
   #### sudo dnf -y install oraclelinux-developer-release-el8
   #### sudo dnf install python36-oci-cli

   5.2 Configuracion del usuario en el Sistema Operativo

   #### Conectarse a la VM por SSH y ejecutar el siguiente comando:

   #### oci setup config

   #### Seguir el flujo del comando

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/API-Key-create-2.jpg)

   5.3 Crear API Key en OCI para configuracion de conectividad via API

   #### Menu Configuracion del usuario>User Setting

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/API-Key-create-1.jpg)

   #### Menu Inferior>API Keys

   #### Copiar la llave publica creada en el paso anterior en el siguiente path: /home/opc/.oci/okit-demo-keys_public.pem

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/API-Key-create-3.jpg)

   #### Crear API Key
   #### Menu Configuracion del usuario>User Setting>Menu Inferior>API Keys

    ![](https://github.com/johncdoracle/OKIT/blob/main/Images/API-Key-create-4.jpg)
    
   #### Revision del archivo config y la informacion del API Key file
   #### Conectarse a la VM por SSH y ejecutar los siguientes comandos:
   #### more /home/opc/.oci/config

   #### Debe coincidir con la informacion del API Key
   #### Menu Configuracion del usuario>User Setting>Menu Inferior>API Keys
   #### Seleccionar la llave recien creada y dar click en View Configuration File

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/API-Key-create-5.jpg)


7. Creacion de la imagen de docker de OKIT

   6.1 Compilacion y crecion de la imagen desde el repositorio de git
   
    #### Conectarse a la VM por SSH y ejecutar el siguiente comando:
    #### sudo dnf install git
    ### docker build --tag okit --no-cache --force-rm https://github.com/oracle/oci-designer-toolkit.git
    ### Revisar la correcta creacion de la imagen con el comando: docker images

   6.2 Ejecuion de la imagen de docker y pruebas

   #### Conectarse a la VM por SSH y ejecutar el siguiente comando:
   #### docker run -d --rm -p 80:80 --volume /home/opc/.oci:/root/.oci --volume /home/opc/.ssh:/root/.ssh --name okit-demo okit
   #### Para revisar la ejecucion del contanedor en el sitema operativo comando: docker ps
   #### Realizar pruebas desde la IP publica de la VM
  
   #### Vista de la herramienta en la UI

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/Okit-demo-run.jpg)


   # Vamos a trabajar con OKIT creando una plantilla y ejecutadola en el Resource Manager de OCI !
   

   

   
   
   
   

   

   
   

   

   
   

    

   

   
   

