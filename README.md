### Proyecto en Arduino

------------

#### Integrantes

------------
- Daraio Camila.
- Dominguez Franco.

 
#### Proyecto contador Binario.

------------

[![Captura-de-pantalla-2023-10-22-203422.png](https://i.postimg.cc/8CZbgD0v/Captura-de-pantalla-2023-10-22-203422.png)](https://postimg.cc/wtsNhKHx)

####  Descripcion

------------


Hemos realizado modificaciones en la primera parte del proyecto, reemplazando los tres botones por un interruptor deslizante. Ahora, el Arduino muestra los números del 0 al 99 en los visualizadores de 7 segmentos de forma automática, sin necesidad de los botones. Además, si utilizamos la otra opción del interruptor, el Arduino mostrará los números primos.

En la segunda parte hemos añadido un sensor de temperatura y un motor de corriente continua al Arduino. Esto nos permite controlar la temperatura y evitar el sobrecalentamiento. Cuando el sensor detecta una temperatura elevada, el motor se enciende, y al mismo tiempo, se activa un LED rojo como indicador de advertencia.

En la fase final de nuestro proyecto, hemos incorporado un LED y una fotoresistencia para detectar la variación en la intensidad luminosa. Esta fotoresistencia actúa como un sensor que reacciona a la presencia o ausencia de luz. Cuando el entorno tiene una mayor cantidad de luz, el LED se apaga automáticamente. Por el contrario, en condiciones de poca luz, el LED se enciende, permitiéndonos adaptar la iluminación a las condiciones ambientales.

------------


####  Funcion principal

------------


La función principal de este proyecto es operar un visualizador de 7 segmentos mediante un interruptor deslizante conectado a una placa Arduino. Este proyecto tiene dos objetivos clave. En primer lugar, muestra números primos del 0 al 99 y, en segundo lugar, cuando el interruptor se desliza, muestra un contador que va del 0 al 99.

Adicionalmente, hemos incorporado un motor que se activa cuando un sensor detecta una temperatura elevada. Cuando esto ocurre, un LED rojo se enciende como indicador de advertencia.

Por último, hemos añadido una fotoresistencia que ajusta una luz LED según la cantidad de luz ambiental. Cuando la luz ambiental disminuye, la LED se enciende, y viceversa.

Para lograr esta interacción, utilizamos directivas #define para asignar nombres descriptivos a los pines y constantes asociados:

Los pines del visualizador de 7 segmentos (B13, A12, F11, G10, E9, D8, C7) simplifican la conexión.
El pin del interruptor deslizante está asignado a un pin específico de la placa Arduino (4).
Los pines UNIDAD (A4) y DECENA (A5) se utilizan para conectar las unidades y decenas del visualizador.
Los pines para las LEDs se definen en la placa Arduino (2, 3).
La fotoresistencia se define en el pin A1.
El motor se conecta al pin 5.
APAGADOS (0) se usa para apagar todos los segmentos del visualizador.
TIMEDISPLAYON (10) regula la duración de visualización de cada número en el display.
El bucle loop() realiza múltiples tareas. En primer lugar, verifica el estado del interruptor deslizante y aumenta el contador o muestra números primos en el visualizador según la posición del interruptor.

Luego, se monitorea la temperatura con el sensor y se activa el motor y el LED rojo si se supera un umbral de temperatura.

Por último, se utiliza la fotoresistencia para detectar la cantidad de luz ambiental y se enciende una LED verde si la luz es insuficiente.

Este proyecto combina diversas funciones para interactuar con varios dispositivos y sensores, proporcionando una experiencia multifuncional




```cpp

void loop() {
  
  currentSwitchState = digitalRead(4);

  if (currentSwitchState == LOW && lastSwitchState == HIGH) {
    countDigit = (countDigit + 1) % 100;
    if (esPrimo(countDigit)) {
    // Muestra el número primo en el display
    printCount(countDigit);
    }
  } 
  else 
  {  
	countDigit = (countDigit + 1) % 100;
    printCount(countDigit);
  }
  
  medida=analogRead(ntc);
  monitoriza();
  if (medida>nivel){
    digitalWrite(led_rojo,HIGH);
    digitalWrite(motor,HIGH);}
   else{
      digitalWrite(led_rojo,LOW);
      digitalWrite(motor,LOW);
  } 
  
  valor = analogRead(fotoresistencia);
  Serial.println(valor);
    delay(500);
  if (valor>100)
  {
    digitalWrite(led_verde,HIGH);
  }
  else
  {
    digitalWrite(led_verde , LOW);
  }
}
```


###### Link del proyecto

------------

- https://www.tinkercad.com/things/ia1V8QD9i3O-parte-3-tp1-cami-daraio/editel?sharecode=Td9U27x70GxINteGlH-4vw6E3NyYpCbazUNr8xLIlqE


------------

###### Fuentes

- https://www.youtube.com/watch?v=_Ry7mtURGDE&t=1927s

------------
