---
description: Por Julia Saenz
---

# Detección del cuerpo con Processing

**Palabras clave**: Sensado del cuerpo, Processing, OSC

{% tabs %}
{% tab title="Conocimientos" %}
* Conocimiento básico de paradigma de objetos
{% endtab %}

{% tab title="Requerimientos" %}
Software

* Processing 3.5.4 o más
{% endtab %}

{% tab title="Links" %}
{% embed url="https://processing.org/" %}

{% embed url="https://sojamo.de/libraries/oscp5/" %}
{% endtab %}
{% endtabs %}

Esta página describe un sistema para sensar el cuerpo usando Processing. La idea es realizar una estructura que pueda adaptarse a diferentes cámaras, métodos se sensado y necesidades, para lo cuál vamos a dividir el código en dos clases principales: `Cámara` y `Detector`&#x20;

La ventaja de este sistema es que ambas partes funcionan independientemente, por lo que se puede modificar una sin modificar la otra y se pueden modificar ambas sin tener que cambiar el código principal.&#x20;

Las subpáginas expanden sobre distintas implementaciones del `Detector` con diferentes tecnologías de sensado del cuerpo, por lo que en está parte nos vamos a centrar en el funcionamiento del programa principal y las estructuras generales de ambas clases.

#### Camara - La entrada de datos

La `Camara` se encarga de elegir la fuente, hacer las configuraciones necesarias, aplicar efectos (si fuese necesario). Las variables y el contenido de los métodos pueden ir variando según la cámara que se conecte, pero mientras los nombres de los métodos y los tipos de datos que retornan se mantengan, el resto del sistema no se va a ver afectado.

Los métodos principales son:

* `mostrarFeed` muestra en pantalla la imagen
* `enviarFeed()` retorna la imagen capturada de tipo `PImage`
* `frenarFeed()` detiene la captura&#x20;

Para crear una instancia de esta clase en el programa principal escribimos:

```processing
Camara cam = new Camara(this);
```

El `this` refiere al sketch sobre el que se va a ejecutar la cámara, en este caso, el programa principal.

#### Detector - El sensado del cuerpo

El `Detector` es el encargado de hacer el sensado del cuerpo usando alguna librería o conectándose a algún programa externo. Al igual que la `Camara` tanto variables y el contenido de los métodos puede variar, mientras se mantengan los métodos usados en el programa principal.

En este caso es probable que también haya nuevos métodos privados a la clase ( ver detección con OpenCV )  pero el método importante es uno:

* `medicion( PImage feed)` recibe el feed y realiza la detección&#x20;

Para crear una instancia de esta clase en el programa principal escribimos:

```processing
 Detector det = new Detector();
```

El constructor también puede variar según el método de detección que se este usando

#### El programa principal

El programa principal, para hacer la detección, solo necesita el siguiente código:

```processing
Camara cam;
Detector det;

void setup(){
    size(640, 480);
    background(0);
    
    cam = new Camara(this);
    det = new Detector();
}

void draw(){
    cam.mostrarFeed();
    det.medicion(cam.enviarFeed());
}

```
