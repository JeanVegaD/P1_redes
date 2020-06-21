---
title: "Documentación"
author: "Jean Vega Díaz"
output: pdf_document
--- 


<img src="https://tecdigital.tec.ac.cr/servicios/capacitacion/guia_estudiantes/resources/images/tec.png" width="250">

**Instituto Tecnológico de Costa Rica**

Centro Académico de Limón  
Escuela de Computación  
Redes 
Proyecto  I  

**Estudiante:**  
Jean Anthony Vega Díaz (2016009280)  


**Profesor:**  
Ing. Johel Godinez Benavides



## Diseño de red

### Conexiones en Packet Tracer

Las virtualziacion de las redes fue realizada en el programa Cisco Packet Tracer y fue realizada de la sigueinte manera:

#### Elementos utilizados 

- 3 `Router 2901`
- 6 `Switch 2960`
- 12 `Laptods`
- 2 `Server-PT`

A 2 de los routers fue necesario incluirles el modulo `HWIC-2T` para permitir las conexiones mediante el puerto serial de tipo `0/0/0`.

Los cables utilizados fueron el `Serial DCE` para las conenexiones entre routers y el `Copper Cross-Over` para el resto de conexiones

#### Conexiones 

En la siguiente ilustracion se detalla la topologia realizada en la herramienta junto con los puertos utilizados para las conexiones.  


![Conexiones realizadas](./assets/conexiones.PNG)


#### Comandos 

##### **VLANS**

Tibas, Uruca, Garita, Coyol, San Rafael, San Joaquin

``` bash
interface vlan 10
description Datos
no shutdown
exit

```
``` bash
interface vlan 20
description Soporte
no shutdown
exit
```

- - - 


##### **Asignacion de puertos**


Tibas, Uruca, Garita, Coyol, San Rafael, San Joaquin

``` bash
interface range fa0/2 - fa0/12
switchport mode access 
switchport access vlan 10
exit
```

``` bash
interface range  fa0/13 - fa0/24
switchport mode access 
switchport access vlan 20
exit
```

- - - 

##### **Trunks**

Tibas, Uruca, Garita, Coyol, San Rafael, San Joaquin

``` bash
interface fa0/1
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 10,20
exit
```
- - - 

## Subneteo

Para realizar la distirbucion se brindo la siguiente red `10.15.0.0/16`

## Showrun 