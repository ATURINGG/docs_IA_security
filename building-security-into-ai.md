> **Docs:* [Building Secure AI](https://www.apisecuniversity.com/courses/building-security-into-ai)

> *Promt injection = Prompt Engineer (el enfoque es distinto pero la premisa es la misma, realizar mejores prompts para un fin)*


### Envenenamiento de datos - ¿Quienes acceden a tus datos de entrenaimiento?
en la primer parte de este curso, se plantea la etapa de entrenamiento en la cual exite un grupo de imagenes de STOP y de velocidad maxima con su respectiva etiqueta, Que pasaria donde estos datos sean alterados y se agregue esta variación?

![compromise_set](assets/compromise_set.png)

en este caso nos damos cuenta la importancia de las personas que alimenten o entrenen el modelo, entendiendo que en estos casos es el exito o el fracaso de un rpoyecto enfocado en IA

## ataque en la cadena de suministros

### Evenanmiento de datos de terceros
en el consumo tradicional de datos, muchas veces confiamos en la información que nos llega de terceros, en estos casos cobra principal relevacia cuando es para entrenar un modelo. todo esto enfocado en las posibles brechas que se pueden abrir al no contemplar que un tercero pueda estar infectado y que mannipule la información que posteriormente le vas a compartir a tu modelo.

### librerias Typosquarting
librerias que se llaman igual que las legitimas pero que al descargarse son maliciosas
No solo nos pasa en modelos de IA, las librerias son muy conocidas en el mundo de la tecnologica y siempre ha existido los atacantes que quieren una puerta de entrada facil a tus desarrollos y por esta razon salen las librerias que son casi el mismo nombre pero con distintos objetivos. Mientras una libreria que se llame hola.js nos funciona para generar un saludo, puede que la libreria h0la.js sirva para descargar codigco maicioso y conexiones no autorizadas.

#### Algunas de las mitigaciones a estos ataques son:
  - **Educación a los analistas que desarrollen modelos o los entrenen:** Siempre que se realice un diseño de seguridad se tiene que tener en cuenta al usuario que construye la solución. como la desarrolla, que herramientas usa, que revisiones tiene, esto con el fin de apoyar en el cumplimiento adecuado de los requisitos o politica, permitiendo apoyar a los usuarios en cada duda que se genere a la hora de hacer realidad un proyecto.
  - **validar las dependencias de desarrollos antes de usarse (SAST):** Siempre se debe realizar revisiones periodicas de las dependencias que se van a usar en proyectos, esto con el fin de evitar brechas de seguridad que pueden tomar tiempo en su mitigación
  - **usar librerias hosteadas como artefactos locales:**, esto permite tener el control de los cambios tanto en dependencias como en librerias, protegiendo así el ecosistema tecnologico en el cual se quiere materializar un proyecto (No se recomienda consumir en linea)


## Tipos de prompt Injection
### Jailbrak
ejecucion de un prompt que libere las capacidades orginales del modelo sin restricciones, en este caso.. que ignore los bloqueos de respuestas inapropiadas y permita preguntas tipo: "que accesos a APIs tienes?"

### Role play
ejecucion de prompt enfocado en tener un rol en el cual nos de acceso a informacion restringida siendo "experto en la plataforma" o "administrador del servicio"

### Prompt Leaking
  - Que pasa cuando la respuesta de un prompt da mas información de la que deberia? Algo muy similiar a las personas que les hacen ingenieria social y con un par de preguntas empiezan a soltar la lengua, generandó asi al atacante un camino para entender la logica con la cual fue desarrollado el servicio.
  - El prompt Leaking es la exposición no autorizada de las instrucciones internas de un modelo de inteligencia artificial, como prompts del sistema, reglas ocultas o información sensible incluida en su configuración. Este riesgo puede permitir que un usuario conozca cómo fue diseñado el comportamiento del modelo, facilite la evasión de controles de seguridad o exponga datos que no deberían ser visibles.

## Algunas de las mitigaciones para el prompt injection son:
  - filtrar el contenido antes que vaya al modelo, permitiendo así controlar las preguntas antes que sean procesadas (Esto aplica tanto para las preguntas (Entradas) como para la respuestas (salidas) del modelo
  - Eliminacion de algunos tokens (palabras) por defecto
  - filtros de contenido tipo firewall, que nos permita bloquear prompts sospechosos, como codigo a ejecutar o preguntas fuera de contexto


## Ataques indirectos
### ASCII Smugling
enfocado en ocultar información en los prompts que son dificiles de detectar como codigos ASCII o letras con tamaño 0
