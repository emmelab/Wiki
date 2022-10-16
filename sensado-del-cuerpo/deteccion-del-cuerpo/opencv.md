---
description: >-
  Está página muestra como detectar una parte del cuerpo con OpenCV for
  Processing
---

# OpenCV

**Palabras Clave**

Cascadas de Haar, OpenCV, Visión computacional

{% tabs %}
{% tab title="Conocimientos" %}
* Conocimiento básico del protocolo OSC
* Conocimiento básico de paradigma orientado a objetos
{% endtab %}

{% tab title="Requerimientos" %}
Software

* Processing
* Librería de OSC para Processing
* Librería de openCV para Processing

Hardware

* Cámara web
{% endtab %}

{% tab title="Links" %}
{% embed url="http://atduskgreg.github.io/opencv-processing/reference/gab/opencv/OpenCV.html" %}
{% endtab %}
{% endtabs %}

## Open CV

### ¿Qué es?

OpenCV (Open Source Computer Vision Library) es una librería de visión computacional y machine learning orientada especialmente a aplicaciones de visión en tiempo real.

### OpenCV for Processing

OpenCV for Processing es la librería de OpenCV desarrollada específicamente para ser utilizada con el entorno de programación Processing. Está basada en la versión de OpenCV para Java y tiene soporte para Linux, MacOS y Windows, pero no Android. Las funcionalidades de esta librería son mucho más reducidas que la versión original: puede reconocer diferencias entre dos imágenes para eliminar fondos o detectar nuevos objetos, encontrar líneas, contornos o bordes de una imagen, trabajar con los canales de color de una imagen o detectar algún objeto o parte del cuerpo específica mediante las cascadas de Haar que vienen con la librería o cascadas importadas.

Esta última es la funcionalidad que usaremos para la detección de una parte del cuerpo.

### ¿Cómo funciona?

Acá hablamos de las hermosas cascadas de Haar acá estoy editando verdad

## Detección con openCV y Processing

{% hint style="info" %}
Esta entrada sigue la estructura planteada en la página "Detección del cuerpo con Processing" por lo que se recomienda leerla antes de continuar
{% endhint %}

En este ejemplo vamos a realizar una detección de manos usando la librería OpenCVForProcessing. Para esto vamos a crear una clase `Detector` a la cuál le vamos a pasar la entrada de la cámara web y nos va a retornar la posición de la mano más cercana a la cámara.&#x20;

Empezamos importando la librería, cuya guía de descarga se puede encontrar en su página:

{% embed url="https://github.com/atduskgreg/opencv-processing" %}

#### Creando el Detector

Nuestra clase `Detector` va a tener 4 atributos:

* Un objeto de tipo `openCV`, que es lo que nos va a permitir hacer la detección
* La posición en `x` e `y` de la mano detectada, que inicializamos fuera de la pantalla
* Un objeto de tipo `Timer` que nos permite detectar si no hay nadie en la escena
* Un número de `easing` que permite suavizar el movimiento de la detección

```processing
class Detector { 
    OpenCV opencv; 
    Timer timer; 
    float x, y= -1; 
    float easing = .08;
```

#### Inicializando el Detector

Esta clase va a recibir 2 parámetros:

* El `sketch` sobre el que se va a ejecutar, cuyo nombre corresponde al nombre con el que se guardo el archivo
* Un `String` de la ruta en la que se aloja la cascada

El `sketch` es necesario para indicarle al objeto `OpenCV` donde tiene que realizar la detección, en este caso dentro de nuestra pantalla. Cuando llamemos a la clase `Detector` desde nuestro programa principal le vamos a pasar el parámetro `this` indicando nuestro programa.&#x20;

La ruta indica la ruta absoluta en donde está ubicada la cascada que vamos a utilizar. El librería de openCV tiene incluidas algunas cascadas, pero para detectar manos necesitamos pasar una propia. La desventaja de que pida una ruta absoluta (en lugar de una relativa) es que cada vez que el archivo se mueve de lugar, ya sea dentro de la misma computadora o una distinta, tiene que actualizarse la variable ruta para indicar la nueva posición del archivo.&#x20;

Una vez que tenemos esos parámetros podemos inicializar nuestro `Detector` .

`openCV` recibe el `sketch` y las dimensiones de la cámara, luego se carga la cáscada con la que vamos a hacer la detección mediante el método `.loadCascade(ruta,true);` y el `Timer` lo iniciamos con el tiempo en segundos que tiene que pasar sin cambios en la pantalla para que se detecte que una persona se fue. Dejarlo en 2 o 3 segundos permite asegurarnos que no se pierda el seguimiento de la mano si por algún momento breve falla la detección.

```processing
  Detector(Sensado_OpenCV sketch, String ruta) {
    opencv = new OpenCV(sketch, 640, 480);

    //opencv.loadCascade (OpenCV.CASCADE_FRONTALFACE); //ejemplo de cascada existente
    opencv.loadCascade(ruta, true); // cascada propia

    timer = new Timer(2); //límite para dejar de detectar
  }
```

#### Configurando la detección

Una vez inicializado el objeto `Detector` podemos empezar a configurar la detección de la mano, para lo cual vamos a usar un método que llamaremos `medicion()` que va a recibir el feed (la imagen de la cámara) y va a pasar por cada uno de sus frames la cascada para detectar la presencia de manos en la escena.

Para realizar la detección son necesarios dos métodos del objeto `openCV` :&#x20;

* `.loadImage( imagen )` recibe la escena sobre la que vamos a realizar la detección
* `.detect( ScaleFactor, MinNeighbour, flags, minSize, maxSize )` realiza efectivamente la detección sobre la escena, retornando un arreglo de rectángulos correspondiente a cada instancia de mano detectada

Este último método puede llamarse sin la necesidad de los parámetros indicados, pero no es recomendable ya que estos son los que permiten controlar cómo se está realizando la detección y son la mejor forma de minimizar falsas detecciones.&#x20;

{% hint style="danger" %}
Acá agregar imagen de la diferencia de detección con parámetros y sin parámetros
{% endhint %}

Estos son cada uno de los parámetros, sus función y los parámetros recomendados:

* `ScaleFactor` refiere a cuánto más chico es el sector en el que detecta la cascada cada pasada; el valor por defecto es 1.1, por lo que en cada pasada el sector es 10% más chico que el anterior. Un número más cercano a 1 implica una detección más lenta pero más meticulosa y un número más alejado corresponde con una detección más rápida pero menos precisa
* `MinNeighbours` corresponde con la cantidad mínima de detecciones positivas que tiene que tener una detección para guardarse finalmente en el arreglo. Se recomienda un valor entre 1 y 5, pero dependerá en cada caso
* `flags` solía usarse para especificar distintos modos de detección pero que ahora no se utiliza, por lo que el valor se deja en 0
* `minSize` y `maxSize` estos dos últimos parámetros indican el menor y mayor tamaño en píxeles que puede tener el objeto detectado, pudiendo así eliminar positivos que aparezcan más cerca o más lejos de lo que se espera

```processing
void medicion(PImage feed) {
    opencv.loadImage(feed); // cargar feed
    Rectangle [] deteccion = opencv.detect(1.2, 3, 0, 150, 400);
```

La variable `deteccion` ahora aloja todas las instancias detectadas de manos en nuestra escena. Idealmente, solo se detecta la instancia que nos interesa (en este caso, la mano más grande de la escena), pero como eso no siempre es posible, va a ser necesario hacer un recorte de esa detección.&#x20;

Adicionalmente, vamos a usar el `Timer` para asegurarnos de no perder el seguimiento de la mano antes de tiempo. Para esto preguntamos si se detectó algo (si el arreglo de detecciones tiene elementos) y si es el caso actualizamos el temporizador. Cuándo no está detectando nada (no hay nadie en la escena) deja de actualizarse y si pasa el tiempo indicado (en nuestro caso 2 segundos) podemos asumir con seguridad que no hay nadie en la escena.

```processing
if (deteccion.length > 0) {
      // si se detecta algo
      timer.guardarTiempo(); // reseteo de timer
    } else {
      // si pasó el tiempo sin detección se oculta el punto medio
      if (timer.pasoElTiempo()) {
        x = -1;
        y = -1;
      }
    }
```

Ahora que ya tenemos el arreglo de detecciones y una forma de asegurarnos de no perder un seguimiento antes de tiempo, podemos pasar a elegir qué mano detectada vamos a seleccionar y mostrar en pantalla. Esto lo vamos a hacer usando 2 métodos:

* `rectMasGrande( deteccion )` nos va a devolver el rectángulo más grande del arreglo
* `puntoMedio( detecccion, i)` va a calcular y dibujar el punto medio del rectángulo

Además tendremos un método con el cuál podemos ver todas las manos detectadas en tiempo real, con el fin de poder configurar la cascada.&#x20;

El método `medicion()` queda entonces de la siguiente forma:

```processing
void medicion(PImage feed) {
    opencv.loadImage(feed); // cargar feed

    Rectangle [] deteccion = opencv.detect(1.2, 3, 0, 150, 400);
    if (deteccion.length > 0) {
      // si se detecta algo
      timer.guardarTiempo(); // reseteo de timer
    } else {
      // si pasó el tiempo sin detección se oculta el punto medio
      if (timer.pasoElTiempo()) {
        x = -1;
        y = -1;
      }
    }
    //mostrarDeteccion(deteccion);
    int i = rectMasGrande(deteccion);
    puntoMedio(deteccion, i);
  }
```

#### Mostrando todas las detecciones

El método `mostrarDeteccion( deteccion )` recibe el arreglo de rectángulos y muestra todas las instancias detectadas. Es usado solamente para calibración, por lo que es privado a la clase.

```processing
private void mostrarDeteccion(Rectangle[] det) {
    for (int i=0; i < det.length; i++) {
      noFill();
      strokeWeight(3);
      stroke(0, 255, 0);
      rect(det[i].x, det[i].y, det[i].width, det[i].height);
    }
  }
```

#### Seleccionando la mano correcta

El método `rectMasGrande( deteccion )` recorre el arreglo de detecciones y devuelve solamente el índice de aquel rectángulo de mayor tamaño, es decir, la detección que es más cercana a la cámara.&#x20;

```processing
  private int rectMasGrande(Rectangle[] det) {
    /* De todos los rectangulos, se queda con el más grande */
    int max = -1;
    if (det.length > 0) {
      int max_tam = -1;
      for (int i= 0; i<det.length; i++) {
        if (det[i].width > max_tam) {
          max = i;
          max_tam = det[i].width;
        }
      }
    }
    return max;
  }
```

#### Calculando el punto medio

Una vez que sabemos el índice del rectángulo que vamos a usar, lo pasamos al método `puntoMedio( deteccion, indice)` y este se va a encargar de calcular el punto medio del rectángulo, suavizar el movimiento de la detección y dibujarlo en pantalla.

```processing
private void puntoMedio(Rectangle[] det, int max) {
    /* Guardar el punto medio del rectangulo con suavizado de movimiento */
    if ( det.length > 0 && max != -1) {
      float ax = (det[max].x + det[max].width/2) - x;
      float ay = (det[max].y + det[max].height/2 + 20) - y;
      x += ax * easing;
      y += ay * easing;
    }
    /* Vizualizar punto medio */
    pushStyle();
    noStroke();
    fill(255, 0, 0);
    ellipse(x, y, 15, 15);
    popStyle();
  }
```

#### Usando el Detector

Ahora que ya tenemos nuestro `Detector` configurado, podemos usarlo en nuestro programa principal de la siguiente forma:

```processing
void setup() {
  size(640, 480);
  background(0);

  c = new Camara(this);
  o = new Detector(this, "C:/Users/Documents/GitHub/Hand.Cascade.1.xml");
}

void draw() {
  c.mostrarFeed();
  o.medicion(c.enviarFeed());
}
```

Una versión de este código está disponible en GitHub

{% embed url="https://github.com/juliasaenz/Sensado-del-cuerpo/tree/main/Processing/Sensado_OpenCV" %}

## Referencias y bibliografía relacionada

Documentación de openCV for Processing

{% embed url="http://atduskgreg.github.io/opencv-processing/reference/gab/opencv/OpenCV.html" %}
