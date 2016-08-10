## Demo 1

El software de demostración consiste en el reconocimiento de un tablero de ajedrez y su reproducción 3D. 

La estructura lógica del mismo se compone de:

  - Una base de datos de objetos conocidos en los cuales almacene el flujo de eventos necesarios para el reconocimiento un tablero de ajedrez. 
  - Un nodo de Mock que lo que haga sea leer el archivo AER provisto por la camara DVS 128 que simule la camara conectada.
  - Un nodo de reconocimiento cuya entrada sea el flujo de eventos y su salida sea el objeto reconocido (modelo).
  - Un nodo que agregue el modelo del objeto reconocido a gazebo.
  
Dicha estructura se puede visualizar en el siguiente diagrama:

![flow](general-flow.jpg)

