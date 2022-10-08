# PrimerAnexo

Lenguaje Multimedial III

TRABAJO PRÁCTICO Nº 5 (Grupal de 7 alumnos)

GUÍA DE TRABAJO

ANEXO

### Integrantes: <a href="#h.jov2lrhl3ru8" id="h.jov2lrhl3ru8"></a>

BILKIS, Carolina - 78529/2

BRAVO, Facundo - 78620/6

NIEVA RODRIGUEZ, Camila - 78990/1

PEREZ DOMINGUEZ, Alvaro - 72315/2

SAENZ, Julia - 78585/0

SÁNCHEZ BARONE, Barbara - 78531/5

SCHÖN, Alejo - 78656/8

### 1. Piezas seleccionadas para el aumento <a href="#h.8id7dsq199nz" id="h.8id7dsq199nz"></a>

&#x20;       Sala vertebrados: Raya moteada

### 2. Idea <a href="#h.kb1rt2udje15" id="h.kb1rt2udje15"></a>

&#x20;       Nuestra idea es crear una experiencia a través de tres plataformas (mapeo, celular e interfaz tangible) e informar sobre la situación actual de la raya moteada con respecto a la influencia del hombre, más específicamente, en relación a la pesca indiscriminada de la especie y cómo, sumado a su ciclo de reproducción lento, ha llevado a que la misma se encuentre en peligro de extinción.

&#x20;       Aprovechamos entonces la realidad aumentada para traer al museo una interpretación de cómo es la pesca, aplicando movimiento y trayendo el entorno al espécimen a través del mapeo, proporcionando información actualizada a través de un dispositivo móvil, y llamando la atención al problema mediante el uso de una red funcionando como interfaz tangible.

### 3. Contenidos <a href="#h.kqnwkeuojrnw" id="h.kqnwkeuojrnw"></a>

#### Estructura general de la experiencia <a href="#h.hmeawureb3f8" id="h.hmeawureb3f8"></a>

&#x20;       Para contar nuestra idea, la estructura que hemos decidido seguir es una serie de 5 instancias que son proyectados en la raya y que son desencadenados por la interfaz tangible o por alguno de los 3 marcadores que se encuentran pegados a la vidriera.

<figure><img src="../../.gitbook/assets/image5" alt=""><figcaption></figcaption></figure>

Diagrama de estados de la experiencia

#### Realidad Aumentada Espacial <a href="#h.het6sya27jgt" id="h.het6sya27jgt"></a>

&#x20;       La realidad aumentada espacial es aquello que es mapeado sobre el espécimen de la raya y la vidriera misma para crear la idea de espacio, entorno y movimiento.

* INSTANCIA PASIVA: Se proyecta el fondo marino sobre la vidriera y la raya se ve quieta, parcialmente enterrada en la arena. La llamamos instancia pasiva porque es lo que se ve antes de que un usuario interactúe de alguna forma con la experiencia.
* INSTANCIA 0: Responde al uso de la interfaz tangible. La raya se mueve ligeramente, y con ese movimiento se desentierra de la arena.
* INSTANCIA 1: Se desencadena cuando el usuario observa el marcador 1. La sombra de una red cubre a la raya, atrapándola, y esta comienza a moverse más rápidamente.
* INSTANCIA 2: Corresponde a la activación del marcador 2. El entorno de la raya cambia del fondo marino y comienza a subir hasta llegar a verse la superficie del mar, dando la impresión de que la raya capturada fue pescada y llevada a la superficie.
* INSTANCIA 3: Desencadenada cuando se activa el marcador 3. La sombra de la red se retira de la raya y esta vuelve al fondo del mar,

#### Realidad Aumentada con Dispositivo - Marcadores y celular <a href="#h.ecpacfq7jjn5" id="h.ecpacfq7jjn5"></a>

&#x20;       Para la realidad aumentada con dispositivo decidimos utilizar marcadores impresos y pegados sobre la vidriera, que pueden ser observados mediante un celular, que muestran unas tarjetas. En estas llamadas tarjetas se presenta la información relevada (la información utilizada en cada tarjeta puede verse detalle en la sección de Fuentes consultadas ) de forma infográfica y accesible de entender para una variedad de usuarios, haciendo uso de texto, imágenes, videos y animaciones. Cada vez que el celular “lee” un marcador con la cámara, manda una señal a la computadora encargada del mapeo para que avance a la instancia correspondiente al marcador.

* TARJETA 1: Corresponde a la información general de la raya. Datos físicos y de su entorno. Se ve un modelo 3D de la raya que ilustra su movimiento.
* TARJETA 2: Información sobre la pesca de la raya moteada. Cómo se pescan, incremento pesquero en los últimos años, valor y lugar de comercialización.
* TARJETA 3: Corresponde a los datos sobre su reproducción y su estado como especie en peligro. Longitud del ciclo, la lista de IUCN.

#### Interfaz Tangible - Red <a href="#h.siakunr8xmak" id="h.siakunr8xmak"></a>

&#x20;       La interfaz tangible es aquella que permite la interacción con información digital (en nuestro caso, el sistema de mapeo) a través de un medio físico. Elegimos para la interfaz simular una red de pesca, de la cual el usuario debe tirar para comenzar la experiencia. Dicha red se encuentra dentro de una caja de aproximadamente 16 cm cúbicos, y la acción de levantarla por parte del usuario manda una señal (utilizando Arduino, un sensor de ultrasonido y una conección de red) a la computadora encargada del mapeo, para que esta haga el pasaje de la instancia pasiva a la instancia 0.

<figure><img src="../../.gitbook/assets/image2" alt=""><figcaption></figcaption></figure>

Funcionamiento de la interfaz tangible

#### Intervención en el espacio <a href="#h.3sl5fcweqrbp" id="h.3sl5fcweqrbp"></a>

&#x20;       La intervención en el espacio cuenta entonces de 4 elementos:

* Proyector, sumado a un soporte.
* 3 marcadores impresos y pegados en la vitrina
* Una caja de aproximadamente 16 cm cúbicos apoyada sobre el estante de la vitrina
* Un teléfono celular, apoyado sobre el mismo estante

<figure><img src="../../.gitbook/assets/image1" alt=""><figcaption></figcaption></figure>

Acercamiento a la intervención en el espacio

### 4. Fuentes consultadas <a href="#h.gc6yh9mf5cj9" id="h.gc6yh9mf5cj9"></a>

#### Información general <a href="#h.rrrsz98d2j80" id="h.rrrsz98d2j80"></a>

&#x20;       Nombre científico: Raja castelnaui

&#x20;       Familia: Rajidae

&#x20;       Nombre común en inglés: spoteback skate

&#x20;       Caracteres externos distintivos: Borde anterior del disco ondulado, hocico romo, con breve saliente en la línea media. Aletas pélvicas con una hendidura poco pronunciada, dos aletas dorsales próximas al extremo de la cola, aleta caudal pequeña. Superficie dorsal cubierta por una espinulación homogénea, áspera al tacto. De 16 a 21 espinas caudales, dispuestas en una única hilera mediana.

&#x20;       Coloración:  Dorso pardo claro y manchas circulares de color marrón oscuro, dispersas regularmente en toda la superficie. Faz ventral blanca, con poros mucosos negros.

&#x20;       Distinción de especies similares en el área: Se distingue fácilmente de las otras rayas por el patrón de coloración del dorso.

&#x20;       Tamaño: La talla máxima observada es de 1,40 m.

&#x20;       Distribución geográfica y comportamiento: Se distribuye desde Río de Janeiro, en Brasil, hasta los 40° S, en Argentina, y desde la costa hasta los 50 m de profundidad.

&#x20;       Formas de utilización: Se utiliza la aleta, pelada o no, congelada, para exportación y en menor proporción para mercado interno.

&#x20;       Entorno: Fondo libre, plantas sólo en la periferia, sin grandes rocas ni terrazas que entorpezcan su desplazamiento. Filtro externo de gran caudal, fondo de grava o arena gruesa. El filtro de placas es prescindible. Se encuentran plantas en la periferia sólo aquellas que desarrollan raíces fuertes y protegidas por rocas (Vallisneria, Sagittaria, Echinodorus)

#### Pesca <a href="#h.rjlrsqibelp2" id="h.rjlrsqibelp2"></a>

Se puede dividir el planeta en cinco categorías teniendo en cuenta el número de especies amenazadas y en el Mar Argentino se determinaron cuatro de ellas: el Río de la Plata (28-30), el área de la Provincia de Buenos Aires hasta el talud aproximadamente (20-27), la zona entre el sur de la Provincia de BuenosAires y 26 Puerto San Julián (Santa Cruz) y hasta las cercanías del talud (12-9) y al sur de esta última abarcando el resto de la plataforma Argentina (6-9)

Las áreas con capturas más elevadas de condrictios,en el Mar Argentino,coinciden con las de más alta diversidad del grupo, colocando a estas zonas en riesgo directo por la práctica de la pesca industrial de arrastre. Esta afirmación está sustentada en el de-crecimiento de cerca del 50% de la biomasa estimada de varias especies ( una siendo la raya a lunares Atlantoraja castelnaui). La disminución de múltiples poblaciones de peces cartilaginosos y óseos y la aparición del efecto de cascada trófica son las consecuencias evidentes de que todo el ecosistema del ASO ha sido afectado con diferentes niveles de impacto por la pesca industrial (Lucifora et al.2011).

Es interesante destacar que son escasos en Argentina los estudios pertinentes para evaluar la sustentabilidad de estas poblaciones teniendo en cuenta los volúmenes de captura de las últimas décadas (Cortés 2007). Además, cabe mencionar que los valores reportados subestiman la mortalidad total de condrictios,por lo que deben considerarse sólo como indicadores de tendencia (Bonfil 1994, Clarke et al.2006b, Worm et al.2013). Las toneladas totales de desembarques reportadas por la FAO no incluyen la captura ilegal no declarada y no reglamentada, ni los descartes a bordo de los buques.

Varias especies de condrictios de la Plataforma Argentina (Callorhinchus callorhynchus, Zapteryx brevirostris, Rhinobatos horkelii, Discopyge tschudii, Squalus acanthias, Atlantoraja castelnaui, A.cyclophora y Psammobatis spp.)han disminuido en al menos el 50% su biomasa estimada, coincidiendo con el incremento del esfuerzo pesquero (12 veces entre 1991 y 1998)de la flota arrastrera (Massa et al.2004)

<figure><img src="../../.gitbook/assets/image4" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image3" alt=""><figcaption></figcaption></figure>

Comercialización

&#x20;       Especímenes de Atlantoraja spp. son comúnmente desembarcados y comercializados en las ciudades de Santos y Guarujá, especialmente los individuos más grandes. Desde 1999 hasta la actualidad, su carne comenzó a exportarse a Asia, especialmente a Corea del Sur (Casarini 2006). La pesca intensiva ha llevado a la sobreexplotación de varias especies de elasmobranquios demersales en el Atlántico sudoccidental (Vooren y Klippel 2005), lo que convierte a Atlantoraja castelnaui en una especie en peligro de extinción (Hozbor et al . 2004). Debido a la sobreexplotación de esta especie, se necesita información actual sobre su biología básica para fines de gestión de poblaciones.

&#x20;       Dulvy y Reynolds (2002) encontraron que las especies de patines que han desaparecido de partes sustanciales de sus áreas de distribución (consideradas como "extintas localmente") tienen tamaños corporales más grandes en comparación con todos los demás patines, ya que un tamaño corporal grande está relacionado con tasas de mortalidad más altas y a los parámetros de la historia de vida, como la edad avanzada en la madurez. Por otra parte, García et al . (2007) también señalaron que (después del modo reproductivo), un gran tamaño corporal aumentó el riesgo de extinción en los elasmobranquios. Esto es motivo de preocupación para A. castelnaui, porque es la especie de patín más grande capturada en el área. Sin embargo, según estos autores, las especies ovíparas estarían sujetas al menor riesgo de extinción que los elasmobranquios con otros modos reproductivos. Además, Frisk et al. (2005) observaron que la fecundidad en la familia Rajidae es mayor que en otros elasmobranquios. Por lo tanto, el riesgo de extinción debido al gran tamaño del cuerpo en esta especie, podría compensarse de alguna manera con la alta fecundidad. Sin embargo, A. castelnaui ya se ha convertido en una especie en peligro de extinción (Hozbor 2004) y esto debe considerarse para fines de gestión y conservación.

#### Crecimiento y reproducción <a href="#h.sf9jl713j52z" id="h.sf9jl713j52z"></a>

En el Golfo San Matías A. platana junto a otras rayas están sometidas a la explotación pesquera es por ello que estimar la edad y el crecimiento es muy importante ya que permite reconstruir la estructura etárea de la población. Más aún si se tiene en cuenta que estos peces dada sus características biológicas son de crecimiento lento. Se analizó la base de datos de FAO de capturas mundiales de los Rajiformes a nivel mundial, a nivel nacional de la Secretaría de Agricultura Ganadería Pesca y Alimentos (SAGPYA) de la Nación Argentina, y a nivel local el Registro de Información Pesquera de la provincia de Río Negro. Se consultó la base de datos de la lista roja de especies amenazadas de la Unión Internacional para la Conservación de la Naturaleza (IUCN su sigla en inglés) y se determinó que A. platana se encuentra categorizada como vulnerable. Las rayas junto con el resto de los condrictios son parte de la fauna acompañante en la captura de la merluza común Merluccius hubbsi que es la especie blanco de la pesquería de arrastre del Golfo San Matías. Se calculó el índice de Captura por Unidad de Esfuerzo (CPUE= Capturas totales Kg/Horas de arrastre) de la flota pesquera de arrastre para las rayas, para la merluza común y el resto de los peces cartilaginosos. En el año 1996 se comienzan a desembarcar las rayas en el golfo, alcanzando su valor máximo en el año 1999 con 343 t. De la comparación de las CPUE entre peces cartilaginosos se observa que antes del año 1996 el pez gallo Callorhinchus callorynchus y el gatuzo Mustelus schmitti presentaban los valores más altos. Para el año 1997 las rayas superan al gatuzo, ocupando el segundo lugar después del pez gallo, quien históricamente fue la especie de condrictio más capturado en el golfo. De la observación de los volúmenes de peces capturados por las lanchas artesanales y los barcos de rada ría los peces cartilaginosos totalizaron 19 t, siendo el gatuzo con alrededor de 8 t el más capturado en el año 2004 y las rayas con 3,6 t en el 2005.

**La lista roja de IUCN**

&#x20;       La lista roja de UICN es un indicador crítico de la salud de la biodiversidad del mundo. Más que una lista de especies y su estatus, es una poderosa herramienta para informar y catalizar acciones por la conservación de la biodiversidad. Provee información sobre el rango, el tamaño de la población, hábitat y ecología, uso y/o comercialización, amenazas, y acciones hacia la conservación de la especie.

&#x20;       La atlantoraja castelnaui es categorizada como “en peligro” (endangered), debido a la pesca y el decrecimiento de población.

#### Fuentes <a href="#h.8p0y7mnmtauc" id="h.8p0y7mnmtauc"></a>

**Información general:**

Cousseau, Figueroa Astarloa. (2000). Clave de identificación de las rayas del litoral marítimo de Argentina y Uruguay. Recuperado en: [https://www.oceandocs.org/bitstream/handle/1834/2505/INIDEP%20Clave%20de%20Rayas.pdf?sequence=1](https://www.google.com/url?q=https://www.oceandocs.org/bitstream/handle/1834/2505/INIDEP%2520Clave%2520de%2520Rayas.pdf?sequence%3D1\&sa=D\&source=editors\&ust=1665265026125179\&usg=AOvVaw3CJMHIH6Vz3AcOfiRkFJ2D)

&#x20;Inidep. Raya a lunares o raya pintada. Recuperado en: [https://www.inidep.edu.ar/wordpress/?page\_id=4380](https://www.google.com/url?q=https://www.inidep.edu.ar/wordpress/?page\_id%3D4380\&sa=D\&source=editors\&ust=1665265026125523\&usg=AOvVaw1aWDH8pJk4xc4iLTK8J3Md)&#x20;

Pesca:

Cuevas. (2016). Herramientas para la conservación de los condrictios costeros del más argentino. Recuperado en: [http://sedici.unlp.edu.ar/bitstream/handle/10915/56249/Documento\_completo.pdf-PDFA.pdf?sequence=](https://www.google.com/url?q=http://sedici.unlp.edu.ar/bitstream/handle/10915/56249/Documento\_completo.pdf-PDFA.pdf?sequence%3D4%26isAllowed%3Dy\&sa=D\&source=editors\&ust=1665265026125962\&usg=AOvVaw30mPZx6mSoS5IHWeRkcJzD)[4\&isAllowed](https://www.google.com/url?q=http://sedici.unlp.edu.ar/bitstream/handle/10915/56249/Documento\_completo.pdf-PDFA.pdf?sequence%3D4%26isAllowed%3Dy\&sa=D\&source=editors\&ust=1665265026126214\&usg=AOvVaw0fnhEr3UNRZpBnLzr3sfbI)[=y](https://www.google.com/url?q=http://sedici.unlp.edu.ar/bitstream/handle/10915/56249/Documento\_completo.pdf-PDFA.pdf?sequence%3D4%26isAllowed%3Dy\&sa=D\&source=editors\&ust=1665265026126442\&usg=AOvVaw1XJWG4CdvuSuu0C6f3O2Hi)&#x20;

Comercialización:

Oddone, Amorim y Mancini.(2008).”Biología reproductiva de la raya a lunares, Atlantoraja castelnaui (Ribeiro, 1907) (Chondrichthyes, Rajidae), en aguas del sudeste brasileño”. Recuperado en: [https://scielo.conicyt.cl/scielo.php?script=sci\_arttext\&pid=S0718-19572008000200010](https://www.google.com/url?q=https://scielo.conicyt.cl/scielo.php?script%3Dsci\_arttext%26pid%3DS0718-19572008000200010\&sa=D\&source=editors\&ust=1665265026126996\&usg=AOvVaw2uB-PrgmQhWQYRgfqdZtqS)

**Crecimiento y reproducción:**

Coller.(2012). Biología, ecología y explotación de la raya platana Atlantoraja platana. Recuperado en: [http://sedici.unlp.edu.ar/handle/10915/23434](https://www.google.com/url?q=http://sedici.unlp.edu.ar/handle/10915/23434\&sa=D\&source=editors\&ust=1665265026127515\&usg=AOvVaw1s7N44sPp6DgM-SAWQk\_on)&#x20;

The IUCN Red List: [https://www.iucnredlist.org/species/44575/10921544](https://www.google.com/url?q=https://www.iucnredlist.org/species/44575/10921544\&sa=D\&source=editors\&ust=1665265026127814\&usg=AOvVaw31xpuc6hJzjTMUG0zwTBsC)&#x20;

**Interfaces de usuario tangibles (TUI):**

Saavedra (s.f.). “UX en Interfaces de Usuario Tangibles”. Recuperado en: [https://medium.com/uxers-umng/ux-en-interfaces-de-usuario-tangibles-f77b4b4ac295](https://www.google.com/url?q=https://medium.com/uxers-umng/ux-en-interfaces-de-usuario-tangibles-f77b4b4ac295\&sa=D\&source=editors\&ust=1665265026128202\&usg=AOvVaw0HxGEOKdT1JFMiWfkmKEB3)&#x20;
