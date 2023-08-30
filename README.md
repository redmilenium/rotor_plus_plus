# rotor_plus_plus
Rotor con azimuth y elevación + Lora (enmarcado dentro de la aventura tinyGS.com)

Como he comentado en la anterior versión, rotor plus, he identificado un problema que afecta a la recepción de la señal de los satelites: la señal Wifi que generan, tanto de la TinyGS como el controlador del rotor, afecta negativamente a la recepción de los satelites, principalmente los que operan cerca de los 400 Mhz.
Supongo que por ser la frecuencia de estos satelites (~ 400 Mhz) un submultiplo de la frecuencia WIFI (~ 2400 Mhz) mas o menos.

Pudiera ser otra la causa, pero alejar la TinyGS de la antena y generar silencio de radio mediante esp_wifi_stop() en la controladora del rotor durante el seguimiento de los satelites, ha mejorado la recepción de estas frecuencias, y obteniendo menor numero de errores de CRC.

He probado tambien a solo separar la TinyGS de la antena, pero al seguir existiendo ruido WIFI cerca de la antena, el de la controladora del rotor, el resultado no mejoraba.

![image](https://user-images.githubusercontent.com/48222471/219964735-e9b03ab3-8a8c-4862-ba71-bbfcd501dcd3.png)

Diagrama de bloques:

![image](https://user-images.githubusercontent.com/48222471/219963042-5a910ad9-36ba-454b-956b-77bf34b30299.png)
Creo que esta es la mejor instalación posible:

1- La TinyGS los mas alejada de la antena + LNA + filtro PasaBanda para que no le afecte a la señal recibida la emisión WIFI de la TinyGS.

2- La tarjeta controladora de los motores de azimuth y elevation, en silencio de radio, es decir solo recibira los datos referente a donde tiene que posicionar los motores. Tambien se le habilitará, en los momentos que no se esta siguiendo ningun satelite, el envio de información como RSSI, SNR, temperatura, etc.

Este es el esquema de la placa con el ESP32. Dependiendo de donde este situada montaremos mas o menos componentes:

![image](https://user-images.githubusercontent.com/48222471/219963378-4f51618b-5d57-4e55-a12d-66700e77d537.png)

Sensores Hall para detectar el posicionamiento cero de Azimuth y Elevation.
![image](https://github.com/redmilenium/rotor_plus_plus/assets/48222471/42dc8794-e372-4689-bfd3-c7b47c55f372)

Vista del detector cero Elevation

![image](https://user-images.githubusercontent.com/48222471/231794455-12560071-c641-43c6-85d1-e8e2d587c228.png)

En la parte del rotor, esta tarjeta debe llevar el ESP32, el modulo LORA, los TMC2209 de control de motores paso a paso y sus componentes asociados (resistencias y condensadores y convertidor cc/cc).

En la parte que estará en casa, solo se necesitará el ESP32, el modulo LORA y los componentes asociados  (resistencias y condensadores y convertidor cc/cc).

Esta placa es muy flexible, de hecho, puede funcionar como TinyGS con los componentes adecuados.
Dejo los archivos de dicha placa listos para enviar a cualquier empresa dedicada a la fabricacion de C.I. (JLCPCB, etc.)

![image](https://user-images.githubusercontent.com/48222471/219966046-f227f057-6386-4066-afda-18ccc9022e40.png)


Con el módulo E22-400M30S puede operar de 410~493MHz - SX1268 RF chip - (ojo porque no se podría sintonizar la ultima hornada de satelites que operan en 400,13 ni la familia FOSSA que operan en 401.7)

Con un modulo E22-900M30S puede operar de 850~930MHz - SX1262 RF chip -

Me pongo a realizar la programación e ire subiendo fotos y resultados a medida que vaya avanzando.

25/02/2023 ya esta realizada la programacion de ambos extremos.

Vista de la pagina WEB servida por el ESP32 instalado en casa y que controla via LORA al ESP32 que se encarga de mover los motores de azimut y elevation.

![image](https://user-images.githubusercontent.com/48222471/221374341-191dabd5-d8c4-4824-a7d7-b8d8a2322108.png)

Lo voy a tener todo montado en casa para realizar las pruebas convenientes antes de proceder a su instalación y evitar contratiempos posteriores.

Vista del sistema de motores paso  del rotor (Azimuth y Elevation) y los detectores de 0:

![image](https://github.com/redmilenium/rotor_plus_plus/assets/48222471/6ee18a5b-68c9-4df7-bd82-c7e071d6ac39)


Vista del controlador del rotor (Azimuth y Elevation):

![image](https://user-images.githubusercontent.com/48222471/221374682-a0b94fe0-2fc1-4f22-a8ab-ef1962c6639c.png)

Se alimenta a 12 voltios, ya que necesita poder mover los motores paso a paso. El ESP32 y el modulo LORA se alimentan a 5 voltios que salen del convertidor de CC/CC.

10/04/2023 -> ya esta instalado el nuevo sistema en el tejado:

![image](https://user-images.githubusercontent.com/48222471/230955860-d7cad3e2-adc7-40ea-bcfe-669ab9abc24b.png)

![image](https://user-images.githubusercontent.com/48222471/230956003-ce19a738-85c5-4e5d-8844-98d09d81516f.png)

A ver ahora como se comporta y si tengo que reorientar hasta encontrar perfectamente los 0 grados.





