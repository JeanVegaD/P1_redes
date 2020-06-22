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






## Subneteo

Para realizar la distirbucion se brindo la siguiente red `10.15.0.0/16`


Se requiere distirbuir de la sigueinte forma:

| Red      |  Host |
|----------|-------|
| Alajuela | 15800 |
| Heredia  | 3800  | 
| San Jose | 900   |
| Enlace 1 | 2     | 
| Enlace 2 | 2     | 




### Procedimiento red `Alajuela`

**Mascara actual**

```
11111111 11111111 00000000 00000000  
255.255.0.0
```

**Formula**

```
2^m - 2 >= host
2^14-2=16382
```

**Nueva Mascara**

```
11111111 11111111 11000000 00000000
255.255.192.0
```

**Salto de red**
```
256-192=64
```
---

A su vez a `Alajuela` se divide de la sigueinte forma:

| Red      |  Host |
|----------|-------|
| Garita   | 8000  |
| Coyol    | 7800  |


**Garita**

**Mascara actual**

```
11111111 11111111 11000000 00000000 
255.255.192.0
```

**Formula**

```
2^m - 2 >= host
2^13-2=8190
```

**Nueva Mascara**

```
11111111 11111111 11100000 00000000
255.255.224.0
```

**Salto de red**
```
256-224=32
```

---

**Coyol**

**Mascara actual**

```
11111111 11111111 11000000 00000000 
255.255.192.0
```

**Formula**

```
2^m - 2 >= host
2^13-2=8190
```

**Nueva Mascara**

```
11111111 11111111 11100000 00000000
255.255.224.0
```

**Salto de red**
```
256-224=32
```

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Garita  | 10.15.0.0        | 10.15.0.1          | 10.15.31.254      | 10.15.31.255  | 255.255.224.0/19   |      
|Coyol   | 10.15.32.0       | 10.15.32.1         | 10.15.63.254      | 10.15.63.255  | 255.255.224.0/19   | 


A su vez `Garita` se divide en  2 redes para los vlans


| Red      |  Host |
|----------|-------|
| Datos    | 4000  |
| Soporte  | 4000  |


**Datos**

**Mascara actual**

```
11111111 11111111 11100000 00000000
255.255.224.0
```

**Formula**

```
2^m - 2 >= host
2^12-2=4094
```

**Nueva Mascara**

```
11111111 11111111 11110000 00000000
255.255.240.0
```

**Salto de red**
```
256-240=16
```

---

**Soporte**

**Mascara actual**

```
11111111 11111111 11100000 00000000
255.255.224.0
```

**Formula**

```
2^m - 2 >= host
2^12-2=4094
```

**Nueva Mascara**

```
11111111 11111111 11110000 00000000
255.255.240.0
```

**Salto de red**
```
256-240=16
```

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Datos   | 10.15.0.0        | 10.15.0.1          | 10.15.15.254      | 10.15.15.255  | 255.255.240.0/20   |      
|Soporte | 10.15.16.0       | 10.15.16.1         | 10.15.31.254      | 10.15.31.255  | 255.255.240.0/20   | 


A su vez `Coyol` se divide en  2 redes para los vlans


| Red      |  Host |
|----------|-------|
| Soporte  | 4000  |
| Datos    | 3800  |



**Soporte**

**Mascara actual**

```
11111111 11111111 11100000 00000000
255.255.224.0
```

**Formula**

```
2^m - 2 >= host
2^12-2=4094
```

**Nueva Mascara**

```
11111111 11111111 11110000 00000000
255.255.240.0
```

**Salto de red**
```
256-240=16
```
---

**Datos**

**Mascara actual**

```
11111111 11111111 11100000 00000000
255.255.224.0
```

**Formula**

```
2^m - 2 >= host
2^12-2=4094
```

**Nueva Mascara**

```
11111111 11111111 11110000 00000000
255.255.240.0
```

**Salto de red**
```
256-240=16
```

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.32.0       | 10.15.32.1         | 10.15.47.254      | 10.15.47.255  | 255.255.240.0/20   |      
|Datos	 | 10.15.48.0       | 10.15.48.1         | 10.15.31.254      | 10.15.31.255  | 255.255.240.0/20   | 





### Procedimiento red `Heredia`

**Mascara actual**

```
11111111 11111111 00000000 00000000  
255.255.0.0
```

**Formula**

```
2^m - 2 >= host
2^12-2=4094
```

**Nueva Mascara**

```
11111111 11111111 11110000 00000000
255.255.240.0
```

**Salto de red**

```
256-240=16
```

---

A su vez a `Heredia` se divide de la sigueinte forma:

| Red           |  Host |
|---------------|-------|
| San Joaquin   | 2000  |
| San Rafael    | 1800  |


**San Joaquin**

**Mascara actual**

```
11111111 11111111 11000000 00000000 
255.255.240.0
```

**Formula**

```
2^m - 2 >= host
2^11-2=2046
```

**Nueva Mascara**

```
11111111 11111111 11111000 00000000
255.255.248.0
```

**Salto de red**
```
256-248=8
```
---

**San Rafael**

**Mascara actual**

```
11111111 11111111 11000000 00000000 
255.255.240.0
```

**Formula**

```
2^m - 2 >= host
2^11-2=2046
```

**Nueva Mascara**

```
11111111 11111111 11111000 00000000
255.255.248.0
```

**Salto de red**
```
256-248=8
```

10.15.64.0

|Nombre       | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|-------------|------------------|--------------------|-------------------|---------------|--------------------|
|San Joaquin  | 10.15.64.0       | 10.15.64.1         | 10.15.71.254      | 10.15.71.255  | 255.255.248.0/21   |      
|San Rafael   | 10.15.72.0       | 10.15.72.1         | 10.15.79.254      | 10.15.79.255  | 255.255.248.0/21   | 


A su vez `San Joaquin` se divide en  2 redes para los vlans


| Red      |  Host |
|----------|-------|
| Soporte  | 1000  |
| Datos    | 1000  |



**Soporte**

**Mascara actual**

```
11111111 11111111 11111000 00000000
255.255.248.0
```

**Formula**

```
2^m - 2 >= host
2^10-2=1022
```

**Nueva Mascara**

```
11111111 11111111 11111100 00000000
255.255.252.0
```

**Salto de red**
```
256-252=4
```
---

**Datos**

**Mascara actual**

```
11111111 11111111 11111000 00000000
255.255.248.0
```

**Formula**

```
2^m - 2 >= host
2^10-2=1022
```

**Nueva Mascara**

```
11111111 11111111 11111100 00000000
255.255.252.0
```

**Salto de red**
```
256-252=4
```

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.64.0       | 10.15.64.1         | 10.15.67.254      | 10.15.67.255  | 255.255.252.0/22   |      
|Datos	 | 10.15.68.0       | 10.15.68.1         | 10.15.71.254      | 10.15.71.255  | 255.255.252.0/22   | 


A su vez `San Rafael` se divide en  2 redes para los vlans


| Red      |  Host |
|----------|-------|
| Soporte  | 1000  |
| Datos    | 800   |



**Soporte**

**Mascara actual**

```
11111111 11111111 11100000 00000000
255.255.224.0
```

**Formula**

```
2^m - 2 >= host
2^10-2=1022
```

**Nueva Mascara**

```
11111111 11111111 11111100 00000000
255.255.252.0
```

**Salto de red**
```
256-252=4
```
---

**Datos**

**Mascara actual**

```
11111111 11111111 11100000 00000000
255.255.224.0
```

**Formula**

```
2^m - 2 >= host
2^10-2=1022
```

**Nueva Mascara**

```
11111111 11111111 11111100 00000000
255.255.252.0
```

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.72.0       | 10.15.32.1         | 10.15.75.254      | 10.15.75.255  | 255.255.252.0/22   |      
|Datos	 | 10.15.76.0       | 10.15.76.1         | 10.15.79.254      | 10.15.79.255  | 255.255.240.0/22   | 



### Procedimiento red `San Jose`

**Mascara actual**

```
11111111 11111111 00000000 00000000  
255.255.0.0
```

**Formula**

```
2^m - 2 >= host
2^10-2=1022
```

**Nueva Mascara**

```
11111111 11111111 11111100 00000000
255.255.240.0
```

**Salto de red**

```
256-252=4
```

---

A su vez a `San Jose` se divide de la sigueinte forma:

| Red           |  Host |
|---------------|-------|
| Tibas         | 400   |
| Uruca         | 500   |


**Tibas**

**Mascara actual**

```
11111111 11111111 11111100 00000000 
255.255.252.0
```

**Formula**

```
2^m - 2 >= host
2^9-2=510
```

**Nueva Mascara**

```
11111111 11111111 11111110 00000000
255.255.254.0
```

**Salto de red**
```
256-254=2
```
---

**Uruca**

**Mascara actual**

```
11111111 11111111 11111100 00000000 
255.255.252.0
```

**Formula**

```
2^m - 2 >= host
2^9-2=510
```

**Nueva Mascara**

```
11111111 11111111 11111110 00000000
255.255.254.0
```

**Salto de red**
```
256-254=2
```


|Nombre       | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|-------------|------------------|--------------------|-------------------|---------------|--------------------|
|Tibas  	  | 10.15.80.0       | 10.15.80.1         | 10.15.81.254      | 10.15.81.255  | 255.255.254.0/23   |      
|Uruca 		  | 10.15.82.0       | 10.15.82.0         | 10.15.83.254      | 10.15.83.255  | 255.255.254.0/23   | 


A su vez `Tibas` se divide en  2 redes para los vlans


| Red      |  Host |
|----------|-------|
| Soporte  | 200   |
| Datos    | 200   |



**Soporte**

**Mascara actual**

```
11111111 11111111 1111110 00000000
255.255.254.0
```

**Formula**

```
2^m - 2 >= host
2^8-2=254
```

**Nueva Mascara**

```
11111111 11111111 11111111 00000000
255.255.255.0
```

**Salto de red**
```
256-254=2
```
---
**Datos**

**Mascara actual**

```
11111111 11111111 1111110 00000000
255.255.254.0
```

**Formula**

```
2^m - 2 >= host
2^8-2=254
```

**Nueva Mascara**

```
11111111 11111111 11111111 00000000
255.255.255.0
```

**Salto de red**
```
256-254=2
```

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.80.0       | 10.15.80.1         | 10.15.80.254      | 10.15.80.255  | 255.255.255.0/24   |      
|Datos	 | 10.15.81.1       | 10.15.81.1         | 10.15.81.254      | 10.15.81.255  | 255.255.255.0/24   | 


A su vez `Uruca` se divide en  2 redes para los vlans


| Red      |  Host |
|----------|-------|
| Soporte  | 250   |
| Datos    | 250   |



**Soporte**

**Mascara actual**

```
11111111 11111111 1111110 00000000
255.255.254.0
```

**Formula**

```
2^m - 2 >= host
2^8-2=254
```

**Nueva Mascara**

```
11111111 11111111 11111111 00000000
255.255.255.0
```

**Salto de red**
```
256-254=2
```
---

**Datos**

**Mascara actual**

```
11111111 11111111 1111110 00000000
255.255.254.0
```

**Formula**

```
2^m - 2 >= host
2^8-2=254
```

**Nueva Mascara**

```
11111111 11111111 11111111 00000000
255.255.255.0
```

**Salto de red**
```
256-254=2
```

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.82.0       | 10.15.82.1         | 10.15.82.254      | 10.15.82.255  | 255.255.255.0/24   |      
|Datos	 | 10.15.83.1       | 10.15.83.1         | 10.15.83.254      | 10.15.83.255  | 255.255.255.0/24   | 


### Procedimiento red `Enalce 1`

**Mascara actual**

```
11111111 11111111 00000000 00000000  
255.255.0.0
```

**Formula**

```
2^m - 2 >= host
2^3-2=6
```

**Nueva Mascara**

```
11111111 11111111 11111111 11111000
255.255.255.248
```

**Salto de red**

```
256-248=8
```

### Procedimiento red `Enalce 2`

**Mascara actual**

```
11111111 11111111 00000000 00000000  
255.255.0.0
```

**Formula**

```
2^m - 2 >= host
2^3-2=6
```

**Nueva Mascara**

```
11111111 11111111 11111111 11111000
255.255.255.248
```

**Salto de red**

```
256-248=8
```

### Resumen


|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Alajuela|10.15.0.0         | 10.15.0.1          | 10.15.63.254      | 10.15.63.255  | 255.255.192.0/18   |      
|Heredia | 10.15.64.0       | 10.15.64.1         | 10.15.79.254      | 10.15.79.255  | 255.255.240.0/20   | 
|San Jose| 10.15.80.0       | 10.15.80.1         | 10.15.83.254      | 10.15.83.255  | 255.255.252.0/22   |
|Enlace 1|  10.15.84.0      | 10.15.84.1         | 10.15.84.2        | 10.15.84.3    | 255.255.255.252/29 |
|Enlace 2| 10.15.84.4       | 10.15.84.5         | 10.15.84.6        | 10.15.84.7    | 255.255.255.252/29 |

#### Alajuela 

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Garita  | 10.15.0.0        | 10.15.0.1          | 10.15.31.254      | 10.15.31.255  | 255.255.224.0/19   |      
|Coyol   | 10.15.32.0       | 10.15.32.1         | 10.15.63.254      | 10.15.63.255  | 255.255.224.0/19   | 


**`Garita`**

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Datos   | 10.15.0.0        | 10.15.0.1          | 10.15.15.254      | 10.15.15.255  | 255.255.240.0/20   |      
|Soporte | 10.15.16.0       | 10.15.16.1         | 10.15.31.254      | 10.15.31.255  | 255.255.240.0/20   | 

**`Coyol`**

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.32.0       | 10.15.32.1         | 10.15.47.254      | 10.15.47.255  | 255.255.240.0/20   |      
|Datos	 | 10.15.48.0       | 10.15.48.1         | 10.15.31.254      | 10.15.31.255  | 255.255.240.0/20   | 

---

#### Heredia 

|Nombre       | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|-------------|------------------|--------------------|-------------------|---------------|--------------------|
|San Joaquin  | 10.15.64.0       | 10.15.64.1         | 10.15.71.254      | 10.15.71.255  | 255.255.248.0/21   |      
|San Rafael   | 10.15.72.0       | 10.15.72.1         | 10.15.79.254      | 10.15.79.255  | 255.255.248.0/21   | 


**`San Joaquin`**


|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.64.0       | 10.15.64.1         | 10.15.67.254      | 10.15.67.255  | 255.255.252.0/22   |      
|Datos	 | 10.15.68.0       | 10.15.68.1         | 10.15.71.254      | 10.15.71.255  | 255.255.252.0/22   | 


**`San Rafael`**

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.72.0       | 10.15.32.1         | 10.15.75.254      | 10.15.75.255  | 255.255.252.0/22   |      
|Datos	 | 10.15.76.0       | 10.15.76.1         | 10.15.79.254      | 10.15.79.255  | 255.255.252.0/22   | 


---

#### San Jose 



|Nombre       | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|-------------|------------------|--------------------|-------------------|---------------|--------------------|
|Tibas  	  | 10.15.80.0       | 10.15.80.1         | 10.15.81.254      | 10.15.81.255  | 255.255.254.0/23   |      
|Uruca 		  | 10.15.82.0       | 10.15.82.0         | 10.15.83.254      | 10.15.83.255  | 255.255.254.0/23   | 

**Tibas**

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.80.0       | 10.15.80.1         | 10.15.80.254      | 10.15.80.255  | 255.255.255.0/24   |      
|Datos	 | 10.15.81.0       | 10.15.81.1         | 10.15.81.254      | 10.15.81.255  | 255.255.255.0/24   | 

**Uruca**

|Nombre  | Dirección de red | Primera utilizable | Ultima utilizable | Broadcast     | Mascara            |
|--------|------------------|--------------------|-------------------|---------------|--------------------|
|Soporte | 10.15.82.0       | 10.15.82.1         | 10.15.82.254      | 10.15.82.255  | 255.255.255.0/24   |      
|Datos	 | 10.15.83.1       | 10.15.83.1         | 10.15.83.254      | 10.15.83.255  | 255.255.255.0/24   | 



## Comandos 

#### **VLANS**

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


#### **Asignacion de puertos**


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

#### **Trunks**

Tibas, Uruca, Garita, Coyol, San Rafael, San Joaquin

``` bash
interface fa0/1
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 10,20
exit
```

---

#### **DHCP Router**

``` bash
service dhcp
ip dhcp pool San Joaquin
network 10.15.64.0 255.255.248.0
default-router 10.15.64.1
```

``` bash
service dhcp
ip dhcp pool San Rafael
network 110.15.72.0 255.255.248.0
default-router 10.15.72.1
```

#### **Ruteo entre VLANS**


**San Jose** -  *Tibas*

``` bash
interface ge0/0.10
encapsulation dot1Q 10
ip address 10.15.80.0 255.255.255.0
exit

interface ge0/0.20
encapsulation dot1Q 20
ip address 10.15.81.0 255.255.255.0
exit
```


**San Jose** -  *Uruca*

``` bash
interface ge0/1.10
encapsulation dot1Q 10
ip address 10.15.82.0 255.255.255.0
exit

interface ge0/1.20
encapsulation dot1Q 20
ip address 10.15.83.1 255.255.255.0
exit
```


**Alajuela** -  *Garita*
``` bash
interface ge0/0.10
encapsulation dot1Q 10
ip address 10.15.0.0 255.255.240.0
exit

interface ge0/0.20
encapsulation dot1Q 20
ip address 10.15.16.0 255.255.240.0
exit
```

**Alajuela** -  *Coyol*

``` bash
interface ge0/1.10
encapsulation dot1Q 10
ip address 10.15.32.0 255.255.240.0
exit

interface ge0/1.20
encapsulation dot1Q 20
ip address 10.15.48.0 255.255.240.0
exit
```

**Heredia** -  *San Joaquin*
``` bash
interface ge0/1.10
encapsulation dot1Q 10
ip address 10.15.64.0 255.255.252.0255.255.252.0
exit

interface ge0/1.20
encapsulation dot1Q 20
ip address 10.15.68.0 255.255.252.0
exit
```

**Heredia** -  *San Rafael*
``` bash
interface ge0/0.10
encapsulation dot1Q 10
ip address 10.15.72.0 255.255.252.0
exit

interface ge0/0.20
encapsulation dot1Q 20
ip address 10.15.76.0 255.255.252.0
exit
```

#### **Ruteo**

**San Jose**

``` bash
ip route 10.15.0.0 255.255.224.0 se0/2/1
ip route 10.15.32.0 255.255.224.0 se0/2/1

ip route 10.15.64.0 255.255.248.0 se0/2/0
ip route 10.15.72.0 255.255.248.0 se0/2/0
```

**Alajuela**

``` bash
ip route 10.15.80.0 255.255.254.0 se0/2/0
ip route 10.15.82.0 255.255.254.0 se0/2/0

ip route 10.15.64.0 255.255.248.0 se0/2/0
ip route 10.15.72.0 255.255.248.0 se0/2/0

```

**Heredia**

``` bash
ip route 10.15.80.0 255.255.254.0 se0/2/0
ip route 10.15.82.0 255.255.254.0 se0/2/0

ip route 10.15.0.0 255.255.224.0 se0/2/0
ip route 10.15.32.0 255.255.224.0 se0/2/0


```


## Showrun 