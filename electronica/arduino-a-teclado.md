# Arduino a teclado

**Palabras Clave**

Lenguajes, Arduino, Processing, Traducción


Conocimientos
Conocimiento mínimo de Arduino Conocimiento básico de Processing


Requerimientos
Software

* Arduino IDE
* Processing 3.0 o más

Hardware

* 1 o más botones, finales de carrera o pulsador
* cablecitos
* Arduino UNO, MEGA, NANO




Este artículo describe brevemente cómo se puede usar un Arduino UNO para ejecutar eventos del teclado. Es una alternativa a cambiar el sistema del Arduino por el de un Arduino Leonardo. El enfoque es en convertir strings que llegan por puerto serie en eventos del teclado, usando como interfaz Processing.



## Arduino

A modo de ejemplo, vamos a imaginar que tenemos una serie de botones que cuando son presionados tienen que ejecutar un evento de teclado en una computadora (por ejemplo, sustituir las flechas del teclado).

Para esto, lo que necesitamos hacer es sensar una serie de botones y enviar por puerto serial el dato.

Si tuvieramos un solo botón, el texto se vería algo similar a lo siguiente:

```arduino
// Declaramos los pines de Arduino de cada botón
const int button = 8;

void setup() {
  Serial.begin(9600); // Incializamos el puerto Serial
  while(!Serial){
    ; // Esperamos a que el puerto abra
  }

  // Iniciamos cada Pin
  pinMode(button, INPUT);
}

void loop() {
	// Si el boton está presionado, enviamos por puerto serial la letra "U"
  if(digitalRead( button ) == HIGH){
    Serial.print("U");
  }
}
```



## Processing

Hasta ahora, todo es bastante sencillo. En processing es donde realmente sucede la magia.

Para empezar, necesitamos acceder al puerto, por lo que precisaremos de la biblioteca `Serial`.

```java
import processing.serial.*;

// DECLARAR OBJETO SERIAL
Serial port;
```

En el `setup` de processing, necesitamos incializarla, en este caso, en el puerto `9600`, el mismo que utilizamos en Arduino.

```java
void setup() {
  size(500, 500);
  background(0);

  // INICIALIZAR PUERTO SERIAL
  println(Serial.list());
  if (Serial.list()[0] != null)
    port = new Serial(this, Serial.list()[0], 9600);

	port.clear(); // Vaciamos el puerto preventivamente.
}
```

A continuación, podemos evaluar si todo marcha bien, imprimiendo en consola los valores que lleguen por ese puerto.

```java
void draw() {
  if (port.available()>0) { // Si hay un mensaje en el puerto
    String serialRead = port.readString(); // lo leo
    println(serialRead); // y lo imprimo
  }

  port.clear();  // Al final de cada fotograma, vacío el puerto
}
```

Si conectamos el arduino a la computadora y ejecutamos el sketch, deberíamos ver que se imprime una “_U”._ **Felicitaciones!**



La herramienta que vamos a precisar para ejecutar un evento de teclado que funcione a nivel del sistema operativo es la clase Robot de Java. Como es una clase de Java y no de processing, vamos a ver que aparece código con el que podemos no estar familiarizados. Continuemos paso a paso.

Para empezar, necesitamos incluir tres bibliotecas.

```java
// IMPORTAR BIBLIOTECAS
import java.awt.AWTException; // Necesaria para disparar errores
import java.awt.Robot; // La clase Robot en cuestión
import java.awt.event.KeyEvent; // Los eventos del teclado que ejecutaremos

// DECLARAR ROBOT
Robot r;
```

A continuación, necesitamos incializarla dentro del `setup`. Aquí es donde vamos a necesitar la biblioteca `AWTException`

```java
void setup() {
  size(500, 500);
  background(0);

  // INICIALIZAR PUERTO SERIAL
	( ... )

	// INICIALIZAR ROBOT
  try {
    r = new Robot();
    r.mouseMove(displayWidth/2, displayHeight/2); // Muevo el mouse para probar si funciona
  }
  catch (AWTException e) {
    println("Robot class not supported by your system!");
    println("La clase Robot no tiene soporte en su sistema");
    exit();
  }
}
```



Ahora que ya tenemos todo preparado, podemos empezar a ejecutar eventos. Las dos funciones que vamos a usar son:

`r.keyPress(int KeyEvent)` → simula que se presionó la tecla que se indica

`r.keyRelease(int KeyEvent)` → simula que la tecla se liberó

Como parámetro, no vamos a enviar un entero directamente, puesto que no sabemos qué número corresponde a qué tecla. Lo que vamos a usar son los eventos que importamos previamente. Por ejemplo, para ejecutar la tecla espacio vamos a escribir:

`keyPress(KeyEvent.VK_SPACE)`

La lista completa de las teclas disponibles la pueden encontrar [acá.](https://docs.oracle.com/javase/7/docs/api/java/awt/event/KeyEvent.html)

Cabe aclarar que cada vez que usamos la función `keyPress` la tecla permanece presionada hasta que le indiquemos lo contrario. Por eso es que luego debemos usar la función `keyRelease`. Por ejemplo:

`r.keyRelease(KeyEvent.VK_SPACE);`

Teniendo esto en cuenta, ya podemos empezar a generar eventos del teclado, en función de lo que se recibe por el puerto serial. Solamente tenemos que completar el código que ya habíamos escrito.

```java
void draw() {
  if (port.available()>0) { // Si hay un mensaje en el puerto
    String serialRead = port.readString(); // lo leo
    println(serialRead); // y lo imprimo

		// Devuelve true si la string es igual a "U"
		boolean buttonPressed = serialRead.equals("U");

    if(buttonPressed)
      r.keyPress(KeyEvent.VK_SPACE); // Presiono la tecla
    else
      r.keyRelease(KeyEvent.VK_SPACE); // La libero
  }

  port.clear();  // Al final de cada fotograma, vacío el puerto
}
```



## Felicitaciones!

Si llegaste hasta acá, ya deberías tener funcionando un pequeño sketch que transforma mensajes seriales en eventos del teclado. Sobre esta base se pueden ir planteando variaciones para ejecutar múltiples teclas en base a mensajes diferentes, e incluso varias a la vez. A continuación dejo a modo de ejemplos, dos acercamientos al problema de ejecutar múltiples eventos en un mismo fotograma. El primero es un poco desprolijo pero más explícito en cuanto a su funcionamiento. El segundo implementa una clase propia que ahorra una parte del problema.

*   Código de Arduino para ambos ejemplos

    ```arduino
    // Declaramos los pines de Arduino de cada botón
    const int buttonUp = 5;
    const int buttonDown = 4;
    const int buttonLeft = 2;
    const int buttonRight = 3;

    const int buttonZ = 11;
    const int buttonX = 10;
    const int buttonC = 9;
    const int buttonV = 8;

    void setup() {
      Serial.begin(9600); // Incializamos el puerto Serial
      while(!Serial){
        ; // Esperamos a que el puerto abra
      }

      // Iniciamos cada Pin
      pinMode(buttonUp, INPUT);
      pinMode(buttonDown, INPUT);
      pinMode(buttonLeft, INPUT);
      pinMode(buttonRight, INPUT);

      pinMode(buttonZ, INPUT);
      pinMode(buttonX, INPUT);
      pinMode(buttonX, INPUT);
      pinMode(buttonV, INPUT);
    }

    void loop() {
    	// Cada botón se envía como una parte de una misma string
    	// Si se presionara, por ejemplo, para ir arriba y a la
    	// derecha, processing recibiría la siguiente string:
    	// "U,R,"
    	// De esta forma el usuario puede ejecutar múltiples
    	// eventos en un mismo fotograma.
      if(isButtonPressed( buttonUp )){
        Serial.print("U,");
      }
      if(isButtonPressed( buttonDown )){
        Serial.print("D,");
      }
      if(isButtonPressed( buttonLeft )){
        Serial.print("L,");
      }
      if(isButtonPressed( buttonRight )){
        Serial.print("R,");
      }

      if(isButtonPressed( buttonZ )){
        Serial.print("Z,");
      }
      if(isButtonPressed( buttonX )){
        Serial.print("X,");
      }
      if(isButtonPressed( buttonC )){
        Serial.print("C,");
      }
      if(isButtonPressed( buttonV )){
        Serial.print("V,");
      }
    }

    bool isButtonPressed(int button) {
      return digitalRead(button) == HIGH; // DEVUELVE VERDADERO SI EL BOTON ESTÁ PRESIONADO  
    }
    ```



*   Ejemplo 1 - “Explícito”

    ```java
    ( ... )
    // El setup es el mismo que veníamos trabajando

    void draw() {
      if (port.available()>0) {
        String full = port.readString();
        String s[] = split(full, ',');

        println(full);

        boolean upPressed = false;
        boolean downPressed = false;
        boolean leftPressed = false;
        boolean rightPressed = false;

        boolean zPressed = false;
        boolean xPressed = false;
        boolean cPressed = false;
        boolean vPressed = false;

        for(int i = 0; i < s.length; i++) {
          if(s[i].equals("U")) upPressed = true;
          if(s[i].equals("D")) downPressed = true;
          if(s[i].equals("R")) rightPressed = true;
          if(s[i].equals("L")) leftPressed = true;

          if(s[i].equals("Z")) zPressed = true;
          if(s[i].equals("X")) xPressed = true;
          if(s[i].equals("C")) cPressed = true;
          if(s[i].equals("V")) vPressed = true;
        }
        if(upPressed) r.keyPress(KeyEvent.VK_UP);
        else r.keyRelease(KeyEvent.VK_UP);

        if(downPressed) r.keyPress(KeyEvent.VK_DOWN);
        else r.keyRelease(KeyEvent.VK_DOWN);

        if(rightPressed) r.keyPress(KeyEvent.VK_RIGHT);
        else r.keyRelease(KeyEvent.VK_RIGHT);

        if(leftPressed) r.keyPress(KeyEvent.VK_LEFT);
        else r.keyRelease(KeyEvent.VK_LEFT);

        if(zPressed) r.keyPress(KeyEvent.VK_Z);
        else r.keyRelease(KeyEvent.VK_Z);

        if(xPressed) r.keyPress(KeyEvent.VK_X);
        else r.keyRelease(KeyEvent.VK_X);

        if(cPressed) r.keyPress(KeyEvent.VK_C);
        else r.keyRelease(KeyEvent.VK_C);

        if(vPressed) r.keyPress(KeyEvent.VK_V);
        else r.keyRelease(KeyEvent.VK_V);

      } else {
        r.keyRelease(KeyEvent.VK_UP);
        r.keyRelease(KeyEvent.VK_DOWN);
        r.keyRelease(KeyEvent.VK_LEFT);
        r.keyRelease(KeyEvent.VK_RIGHT);

        r.keyRelease(KeyEvent.VK_Z);
        r.keyRelease(KeyEvent.VK_X);
        r.keyRelease(KeyEvent.VK_C);
        r.keyRelease(KeyEvent.VK_V);
        println(".");
      }

      port.clear();
      // println(".");

    }
    ```
*   Ejemplo 2 - “Elegante”

    ```java
    class Botoino {
      String name;
      int keyEvent;

      Botoino(String _name, int _keyEvent) {
           name = _name;
           keyEvent = _keyEvent;
      }

      void presionarSiEnMsj (String msj) {
        if(msj.indexOf(name) >= 0){
          r.keyPress(keyEvent);
        }else {
          r.keyRelease(keyEvent);
        }
      }

      void soltarTecla() {
        r.keyRelease(keyEvent);
      }
    }

    //---------------------------------------

    // IMPORTAR BIBLIOTECAS
    import java.awt.AWTException;
    import java.awt.Robot;
    import java.awt.event.KeyEvent;

    import processing.serial.*;

    // DECLARAR OBJETO SERIAL
    Serial port;

    // DECLARAR ROBOT
    Robot r;

    // DECLARAR TECLAS
    Botoino arriba;
    Botoino abajo;
    Botoino derecha;
    Botoino izquierda;

    void setup() {
      size(500, 500);
      background(0);

      // INICIALIZAR PUERTO SERIAL
      println(Serial.list());
      if (Serial.list()[0] != null)
        port = new Serial(this, Serial.list()[0], 9600);

      // INICIALIZAR ROBOT
      try {
        r = new Robot();
        r.mouseMove(displayWidth/2, displayHeight/2); // Muevo el mouse para probar si funciona
      }
      catch (AWTException e) {
        println("Robot class not supported by your system!");
        exit();
      }
      port.clear();

      // INICIALIZAR TECLAS
      arriba = new Botoino("U", KeyEvent.VK_UP);
      abajo = new Botoino("D", KeyEvent.VK_DOWN);
      izquierda = new Botoino("L", KeyEvent.VK_LEFT);
      derecha = new Botoino("R", KeyEvent.VK_RIGHT);
    }

    void draw() {
      // SI HAY ALGO EN EL PUERTO SERIAL
      if (port.available()>0) {
        // LA STRING QUE RECIBIMOS POR PUERTO SERIAL
        String serialRead = port.readString();
        println(serialRead);

        // LEEMOS LA STRING Y VEMOS SI EJECUTAMOS LA TECLA O NO
        arriba.presionarSiEnMsj(serialRead);
        abajo.presionarSiEnMsj(serialRead);
        izquierda.presionarSiEnMsj(serialRead);
        derecha.presionarSiEnMsj(serialRead);

      } else {
        arriba.soltarTecla();
        abajo.soltarTecla();
        izquierda.soltarTecla();
        derecha.soltarTecla();

        println(".");
      }

      port.clear();
      // println(".");

    }
    ```



## Fuentes consultadas

[How do I generate a keyPress? (maybe Robot)](https://forum.processing.org/two/discussion/4583/how-do-i-generate-a-keypress-maybe-robot.html)

[Robot (Java Platform SE 7 )](https://docs.oracle.com/javase/7/docs/api/java/awt/Robot.html)

[KeyEvent (Java Platform SE 7 )](https://docs.oracle.com/javase/7/docs/api/java/awt/event/KeyEvent.html)

[Robot Class in Java AWT - GeeksforGeeks](https://www.geeksforgeeks.org/robot-class-java-awt/)
