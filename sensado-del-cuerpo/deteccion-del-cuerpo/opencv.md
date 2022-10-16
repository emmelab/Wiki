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
* Su posición en `x` e `y` que inicializamos fuera de la pantalla
* Un objeto de tipo `Timer` que nos permite detectar cuando una persona se fue
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

Una vez inicializado el objeto `Detector`

#### Mostrando la detección

#### Seleccionando la mano correcta

#### Calculando el punto medio



## Referencias y bibliografía relacionada

Documentación de openCV for Processing

{% embed url="http://atduskgreg.github.io/opencv-processing/reference/gab/opencv/OpenCV.html" %}
