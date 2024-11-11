# Oracle OKIT
Instalacion y Configuracion de OKIT

## Que es OKIT ?

Es un kit de herramientas de diseño y visualización OCI (OKIT) es una herramienta basada en navegador que permite al usuario diseñar, implementar y visualizar (introspeccionar/consultar) entornos OCI a través de una interfaz gráfica basada en web.

### Pasos para la instalación

1. Creacion de la VCN en OCI:
   #### Menú>Networking>Virtual Cloud Networks
   Seleccionamos Start VCN Wizard y seguimos el flujo de creacion asignando el nombre, el rango de CIDR, subnets etc.
     
   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/Start-Wizard.jpg)

   
2. Creacion de Virtual Machine en OCI
   #### Menú>Compute>Instances>Create Instance

   #### Completar informacion de AD, Shape, Imagen, Red y cargar llave SSH

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/VM-create.jpg)


2.1 Crear Internet Gateway
   #### Menú>Networking>Virtual Cloud Networks>Internet Gateways

   Asignar nombre y crear

   ![](https://github.com/johncdoracle/OKIT/blob/main/Images/IGW-create.jpg)
   
2.2 Configurar la Tabla de la Rutas y la SL de la Subred
   #### Menú>Networking>Virtual Cloud Networks>Route Tables

   

5. Actualizacion del Sistema Operativo
   #### Conectarse a la VM por SSH y enviar el comando: sudo dnf update -y 

   

   
   

