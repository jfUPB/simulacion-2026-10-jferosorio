
<img width="986" height="237" alt="image" src="https://github.com/user-attachments/assets/2234e071-34be-4b7c-a6b6-c7a2d20bad25" />

https://natureofcode.com/particles/


# Unidad 5
## Bitácora de proceso de aprendizaje

Podemos crear un sistema de particulas
Podemos crear un sistema de sistemas de particulas, clickear el canvas y generar el sistema de particulas

Herencia y poliformismo. El comportamiento se solicita en su comportamiento a partir de encapsular sus caracteristicas.



### 👌 Actividad 1 Anatomía de una partícula
https://editor.p5js.org/natureofcode/sketches/-xTbGZMim
<img width="611" height="256" alt="image" src="https://github.com/user-attachments/assets/843fd5bc-b54d-4fb0-a2f4-dc5a1fed078d" />



**Capa de comportamiento:**

1. ¿Qué propiedades tiene cada partícula? Clasifícalas: ¿Cuáles definen su estado físico? ¿Cuáles su estado vital?
Estas las podemos ver en el fragmento de codigo
```
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y); //Aqui se establece la posicion donde se crea
    this.acceleration = createVector(0, 0);  // Aqui creamos el comportamiento que tendra el movimiento
    this.velocity = createVector(random(-1, 1), random(-1, 0)); // Aqui creamos la velocidad que inflira en el la aceleracion que estara determinada aleatoriamente en un rango, esto crea un comportamiento variable y natural, hace que todas las particulas no se comprten igual
    this.lifespan = 2550.0; // Aqui creamos el tiempo de vida de la particula
 ```

Esta capa de comportamiento se puede llevar a GPU a tra vez de **compute shaders**  Esto para manejar un garn volumen de particulas




2. ¿Qué condición determina que una partícula “muere”? ¿Es una muerte instantánea o gradual? 
particles.splice(i, 1), Es una muerte gradual determinada a un rango de i y 1. Esta aunque este por fuera del canvas puede seguir viva, pues se esta estableciendo una muerte por edad no por sivualizacion, suceptible de optimizacion

3. ¿Cómo se actualiza la partícula en cada frame? Identifica el patrón motion 101 dentro de la partícula. 

Se encuentra en este fragmento de codigo:
```
  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
 ```   
**Capa de estructura:**

¿Quién crea las partículas? ¿En qué momento?  class Particle {
¿Quién decide cuándo eliminar una partícula del array?
```
 for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.run();
    if (particle.isDead()) {
      //remove the particle
      particles.splice(i, 1); //Esta es la parte que que elimina la particula del array
    }
```
¿Por qué se recorre el array en orden inverso para eliminar? ¿Qué pasaría si no se hiciera así?

<img width="803" height="301" alt="image" src="https://github.com/user-attachments/assets/30b3c3f6-7c7d-45fd-87c7-b87d13594729" />

Se revisa normalmente las posiciones en orden ascendente, pero si una partidula en una posicion intermedia muere, la siguiente particula ocupara su POSICION, pero el rapaso de posiciones continuara, por lo que esta particula que reemplazo a la que murio pasara por alto, en cambio si repasamos el array de forma inversa, si esta situacino se presenta no habra particulas que ocupen nuevas posiciones que sean ignoradas.

Si no eliminaras nunca las partículas, ¿Qué pasaría con la memoria y el rendimiento? Haz el experimento: comenta la línea que elimina y observa el frame rate.
Si no matamos las particulas naturalmente seguiran cosumiendo recursos aunque salgan del rango de visualizacion (canvas), sobrecargando la memoria por el tiempo que se siga ejecutando el programa


**Capa de visualización:**
Se puede llevar a GPU con **Vertex y fragmente shaders** Esto para manejar un garn volumen de particulas

1. ¿Qué elementos visuales usa para representar una partícula?
La partícula se dibuja en el método show() usando:

```
circle(this.position.x, this.position.y, 8); → forma: un círculo
stroke(0, this.lifespan); → borde: color negro con transparencia
strokeWeight(2); → grosor del borde
fill(127, this.lifespan); → relleno: gris con transparencia
```


2. ¿Cómo se conecta el “tiempo de vida” con la apariencia visual?

lifespan afecta directamente la transparencia (alpha):

```
stroke(0, this.lifespan)
fill(127, this.lifespan)

```
3. Si quisieras cambiar la representación visual (por ejemplo, usar líneas en vez de círculos), ¿Qué cambiarías y qué NO cambiarías?

Para lograr que las particulas cambien de circulos a lineas, solo bastaria con editar el show() de la siguiente manera:
```
show() {
  stroke(0, this.lifespan);
  strokeWeight(2);
  line(
    this.position.x,
    this.position.y,
    this.position.x + 10,
    this.position.y + 10
  );
}
```



### 👌 Actividad 2 Del array al sistema: la abstracción del emisor

### 👌 Actividad 03: Heterogeneidad: herencia y polimorfismo

Link de proyecto con mis  notas; https://editor.p5js.org/jferosorio/sketches/HrYAmOiF5
<img width="1662" height="505" alt="image" src="https://github.com/user-attachments/assets/462ec153-4abb-4c89-9f40-28e5d9c2d747" />



📤 Bitácora

¿Qué tienen en común las subclases de partículas? ¿Qué tienen de diferente?

¿Por qué es importante que el Emitter no necesite saber qué tipo específico de partícula está gestionando? Explica esto con tus propias palabras.
Por que esto engloba la revision de todo aquello que se queba en el concepto de Particula, no cuestiona; Es una particula circular?, Es una particula cuadrada?, NO. Solo se limita a trabajar sober lo que le compete, en ete caso que se trate de un Particle

Si mañana quisieras agregar un tercer tipo de partícula, ¿Qué tendrías que crear y qué NO tendrías que modificar?
Esto depende del flujo y la inclinacion que se tenga a la hora de editar el codigo, si quieres optimizar el trabajo colaborativo habra unas formas, si quieres optimizar la gestion de recurso habra otra, en este caso optaremos por dar una respuesta mas cercana a lo segundo, ya que estamos trabajando en un flujo de trabajo individual. 

```
<img width="789" height="189" alt="image" src="https://github.com/user-attachments/assets/36c18bf2-c05a-4824-948a-785d37d82b13" />

Lo que yo haria seria simplemente agregar en esta zona del codigo addParticle(), linea y determinandole una probabilidad

```


Compara con Example 4.2: ¿Cambió la lógica del Emitter? ¿Cambió la lógica de muerte? ¿Qué capa del sistema se modificó y cuáles permanecieron intactas?

Evidentemente vemos cambios estructurales en los emiters, es interesante ver que casualmente nos encontramos en la **Capa de estructura** 


<img width="841" height="671" alt="image" src="https://github.com/user-attachments/assets/34c1d6dd-287d-4cca-af94-b9c04ac61119" />



### Actividad 4; Fuerzas y particulas
https://editor.p5js.org/jferosorio/sketches/2qmO_0mki

Antes teniasmos que la fuerzas estaban directamente en el comportamiento de las particulas.

Ahora tenemos una actualizacion de MOtion 101, 




### La industria...
Apple no va con openGL, entonces crea Metal

WebGPU.
Plataforma web como amplia gama de mercado laboral

"Lenguaje de shaders"

Crear DSLs, lenguaje de dominio, three.js tiene lenguaje DSL. Se tiene un lenguaje, y se traspila a lenguaje de navegador con soporte GPU, si no tiene soporte entonces deja otro lenguaje normi.


## Bitácora de aplicación 

### Actividad 5
Diseñar un "ciclo de vida", algo nace, se trasforma y desaparece.
```
Un ciclo de vida es cualquier proceso donde algo nace, se transforma y desaparece. Puede ser literal (semillas → flores → pétalos que caen), metafórico (ideas → conversaciones → olvido), emocional (calma → agitación → disolución), natural (estrellas → supernovas → polvo cósmico), o social (rumores que se propagan, se fragmentan y mueren).
```

Requisitos conceptuales
1. Dos tipos de particulas diferentes (herencia y poliformismo)
2. Ciclo de vida visible. La muerte no puede ser solo desaparecer, debe comunicar algo
3. Al menos una fuerza que afecte las particulas (gravedad, atraccion, repulsion, viento, u otra)
4. La interaccion del usuario debe tener un proposito narrativo claro
5. Gestion correcta de memoria, las particulas que mueren se eliminan

```
Lo que se evalúa NO es la complejidad técnica del código (eso lo puede generar una IA), sino:

La coherencia entre el concepto de ciclo de vida y las decisiones de diseño.
Que puedas explicar cómo cada elemento del sistema contribuye a comunicar la idea.
Que la pieza transmita algo reconocible al verla e interactuar con ella.
```
## ~~EL VIAJE DE DANTE~~

<img width="922" height="748" alt="image" src="https://github.com/user-attachments/assets/0a065d34-1ba4-42b6-beb3-d0ffe8515f33" />

~~Inspirado en el viaje de Dante a travez de la divina comedia me gustaria plasmar "ciclo de vida" en el proceso de redencion del paso de la humanidad a la eternidad, el paso por los circulos del infieno, el trayecto del purgatorio y la llegada al paraiso. Mi particula principal realizar este viaje mencionado, iniciando en forma de estrella y manchada y con una estela a fin de simular la maldad humana y los pecados, a medida que avanza por la experiencia esta se ira trasformando hasta convertirse en una esfera de color claro. La interaccion que veo posible es que le usuario al dar click cree una nueva particula simulando una nueva vida que pasa al nuevo plano existencial~~


...Otra idea...
## CICLO DEL AGUA

LINK AL PROYECTO: https://editor.p5js.org/jferosorio/sketches/H2HIDIuRU

<img width="1232" height="655" alt="image" src="https://github.com/user-attachments/assets/01bd11f0-e84f-428e-a16c-f1edbf217ebf" />




El sistema representará el ciclo del agua a través de una simulación interactiva en la que el usuario tendrá un papel activo dentro del entorno. Al mantener presionado el mouse, se generará lluvia mediante un emisor de partículas que dará origen a gotas de agua, las cuales serán afectadas por la gravedad y descenderán sobre una montaña. Al entrar en contacto con la superficie, se deslizarán de forma natural según la pendiente del terreno, simulando el comportamiento del agua en los ríos. Una vez lleguen a la base, donde se encontrará el río, las partículas cambiarán de estado y pasarán a representar vapor de agua, el cual ascenderá mientras se desvanece, comunicando visualmente el proceso de evaporación. Este cambio permitirá evidenciar el ciclo de vida de las partículas, evitando que desaparezcan de manera abrupta y reforzando la narrativa del fenómeno natural. Adicionalmente, la simulación incorpora un ciclo de día y noche que aportará dinamismo al entorno, enriqueciendo la experiencia visual.

```
let particulas = [];
let tiempo = 0;
let emitter;

function setup() {
  createCanvas(800, 600);
  emitter = new Emitter();
}

function draw() {
  tiempo += 0.005;

  // Crearemos ciclo de dia y noche
  let dia = map(sin(tiempo), -1, 1, 0, 1);
  let cielo = lerpColor(color(10, 10, 40), color(135, 206, 235), dia);
  background(cielo);

  dibujarEscenario();

  // Emision continua de particulas
  if (mouseIsPressed) {
    emitter.emit(mouseX, mouseY);
  }

  // Actualizar particulas y muerte
  for (let i = particulas.length - 1; i >= 0; i--) {
    let p = particulas[i];
    p.update();
    p.show();

    if (p.muerta()) {
      particulas.splice(i, 1);
    }
  }
}



//Escenario
function dibujarEscenario() {
  // montaña
  fill(80, 180, 80);
  triangle(0, height,0, height / 2, width, height);

  // río
  fill(40, 90, 200);
  rect(0, height - 50, width, 50);
}




// altura de la montaña (colisión)
function alturaMontana(x) {
  let centro = 0;
  let altura = height / 2;

  let dist = abs(x - centro);
  let maxDist = width / 2;

  return map(dist, 0, maxDist, altura, height);
}



// Emisor de gotas de lluvia
class Emitter {
  emit(x, y) {
    for (let i = 0; i < 5; i++) {
      particulas.push(new Gota(x + random(-90, 90), y));
    }
  }
}




//  GOTAS / VAPOR

class Gota {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(random(-0.5, 0.5), random(0, 1)); //Vector aleatorio para comportamiento mas natural
    this.acc = createVector(0, 0);

    this.tamano = random(4,9); // Crearemos gotas de difrente tamano para dar naturalidad
    this.estado = "lluvia";

    this.ruidoOffset = random(1000);
  }

  aplicarFuerza(f) {
    this.acc.add(f);
  }

  update() {
    if (this.estado === "lluvia") {
      let gravedad = createVector(0, 0.2);
      this.aplicarFuerza(gravedad);

      // colision
      let suelo = alturaMontana(this.pos.x);

      if (this.pos.y >= suelo) {
        this.pos.y = suelo;

        // deslizamiento tipo río
        this.vel.y = 0.5;       // evita rebotes raros
        this.vel.x += 0.1;      // flujo lateral
      }

      // cuando llega al rio pasamos a estado de evaporacion
      if (this.pos.y > height - 60) {
        this.estado = "evaporacion";
        this.vel = createVector(0, random(-1.5, -2.5));
      }
    }

    
    
    
    //EVAPORACIÓN
    
    if (this.estado === "evaporacion") {
      let subida = createVector(0, -0.03);
      this.aplicarFuerza(subida);

      let vientoX = map(noise(this.ruidoOffset), 0, 1, -0.5, 0.5);
      this.ruidoOffset += 0.01;

      this.aplicarFuerza(createVector(vientoX, 0));
    }

    //  MOTION101
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show() {
    noStroke();

    if (this.estado === "lluvia") {
      fill(0, 0, 255, 180);
      ellipse(this.pos.x, this.pos.y, this.tamano, this.tamano * 1.5);
    } else {
      fill(220, 220, 255, 120);
      ellipse(this.pos.x, this.pos.y, this.tamano * 1.5);
    }
  }

  muerta() {
    return this.pos.y < 0;
  }
}
```
<img width="793" height="436" alt="image" src="https://github.com/user-attachments/assets/07ca9eb1-340b-46a4-9a37-c794925b02b9" />
<img width="788" height="509" alt="image" src="https://github.com/user-attachments/assets/eff97370-9cca-4980-879e-1da5c040a90b" />
<img width="796" height="497" alt="image" src="https://github.com/user-attachments/assets/79014b58-6a89-4fc5-8dc2-8244afed7bb7" />



### Para resolver los requisitos concpetuales
 
1. Dos tipos de partículas diferentes (herencia y polimorfismo)
Se manejan partículas en dos estados: lluvia y evaporación. Aunque pertenecen a la misma estructura base, su comportamiento cambia según el estado (caer o subir), lo que evidencia el uso de polimorfismo al ejecutar métodos como update() y show() de manera diferente.

2. Ciclo de vida visible
Las partículas no desaparecen de forma inmediata. Primero caen como gotas, luego al llegar al río se transforman en vapor y finalmente ascienden mientras se desvanecen, mostrando claramente el proceso de evaporación antes de “morir”.

3. Fuerzas que afectan las partículas
Se aplican varias fuerzas: la gravedad en la caída, la pendiente de la montaña que dirige el flujo del agua hacia los lados, y una fuerza ascendente con variación lateral (ruido de Perlin) que simula el viento durante la evaporación.

4. Interacción del usuario con propósito narrativo
El usuario, al mantener presionado el mouse, genera la lluvia. Esta acción activa todo el ciclo del agua, dándole sentido narrativo a la interacción dentro de la simulación.

5. Gestión correcta de memoria
Las partículas se eliminan cuando terminan su ciclo de vida (cuando salen del canvas). Esto se hace recorriendo el arreglo en reversa y usando splice, evitando acumulación innecesaria y manteniendo el rendimiento del programa.

---

<br><br><br>

## Otras notas...

Para tener en cuenta
Podemos generar el comportamiento en el show(), de tal manera que cierto rango del tiempoi de vida de la partidcula tenga ciertas caracteristicas, que de 255 a 150 tal cosa, de 150 a 100 de trasforma y de 100 a 0 muere y pasa tal cosa

El run()

en for() realiza el repaso de las posiciones d elas particulas al reves por el -1 por el tema explicado
<img width="1557" height="732" alt="image" src="https://github.com/user-attachments/assets/61d5ec46-ce03-4562-893f-41c49e71c092" />

<img width="803" height="301" alt="image" src="https://github.com/user-attachments/assets/30b3c3f6-7c7d-45fd-87c7-b87d13594729" />

<br><br><br>
---

## 🧠Bitácora de reflexión

## Parte 1 — Principios fundamentales

**Describe con tus propias palabras cada uno de estos 10 principios:**

1. **Una partícula es una entidad con estado:**
   Una partícula es un elemento **individual** que posee propiedades propias que definen su estado en un momento determinado, como posición, velocidad, tamaño, color o energía ETC. Estas características pueden cambiar con el tiempo, lo que permite describir su comportamiento dentro de un sistema.

2. **Una partícula tiene ciclo de vida:**
   Se entiende como ciclo de vida que algo se genera, pasa por un proceso y finalmente desaparece. Por ello, el comportamiento de la partícula obedece a este lineamiento: no es algo que exista de forma atemporal, sino que surge como consecuencia de una acción o condición. De igual manera, se busca que lo que ya no se muestra en escena no consuma recursos; por eso es importante que, una vez finaliza la función de una partícula, esta desaparezca y deje de requerir procesamiento. Esto optimiza el sistema y evita sobrecargar el proyecto con elementos innecesarios.

3. **Un sistema de partículas gestiona colecciones dinámicas de elementos:**
   Existen múltiples variables que se pueden aplicar a una partícula y a su comportamiento. Por eso, un sistema de partículas organiza y controla un conjunto de ellas, permitiendo que interactúen entre sí y generen comportamientos complejos a partir de reglas simples.

4. **La creación y eliminación de partículas no es un detalle técnico menor, sino parte central del modelo:**
   Como se mencionó anteriormente, las partículas tienen un ciclo de vida: deben aparecer y desaparecer. No pueden permanecer indefinidamente en el sistema, ya que esto implicaría un uso innecesario de recursos. Por lo tanto, la gestión de su creación y eliminación es fundamental para el funcionamiento eficiente del modelo.

5. **Debe haber separación entre la lógica de una partícula individual y la lógica del sistema/emisor:**
   No es lo mismo analizar el comportamiento de una partícula individual que estudiar el comportamiento del sistema completo. La lógica de cada partícula define sus propiedades y acciones propias, mientras que el sistema o emisor define cómo se crean, se agrupan y se relacionan con el entorno. Separar estas responsabilidades facilita el diseño, la organización y la escalabilidad del sistema.

6. **Un emisor o particle system es una abstracción importante:**
   El emisor es el encargado de generar y controlar las partículas. Funciona como una abstracción que permite definir cómo, cuándo y dónde se crean, así como sus características iniciales. Gracias a esta abstracción, es posible modificar el comportamiento global del sistema sin necesidad de cambiar cada partícula individual.

7. **Pueden existir sistemas de sistemas:**
   No solo es importante analizar cómo interactúan las partículas dentro de un sistema, sino también cómo diferentes sistemas de partículas interactúan entre sí. Estos sistemas pueden coexistir con comportamientos distintos, por lo que es necesario definir si se complementan, se repelen, funcionan de manera simbiótica o si uno predomina sobre otro.

8. **Puede haber heterogeneidad usando herencia y polimorfismo:**
   No todas las partículas tienen que ser iguales. Mediante el uso de herencia y polimorfismo, es posible definir distintos tipos de partículas que comparten ciertas características, pero que también presentan comportamientos específicos. Esto permite construir sistemas más flexibles y variados.

9. **Las partículas pueden responder a fuerzas globales y locales:**
   Las partículas no actúan de forma aislada, sino que pueden verse afectadas por fuerzas externas. Estas pueden ser globales, como la gravedad o el viento que afecta a todas las partículas, o locales, como interacciones específicas entre partículas o con objetos cercanos. La forma en la que venimos aplicando estas furzas se plasman en principalmente en el sistema de MOTION 101 visto en el trascurso del curso

10. **La representación visual puede variar sin cambiar el principio algorítmico de fondo:**
    La forma en que se visualizan las partículas (color, forma, tamaño, textura) puede cambiar sin alterar el funcionamiento interno del sistema. Es decir, el algoritmo que define su comportamiento puede mantenerse igual, mientras que su apariencia se adapta según las necesidades visuales o estéticas. Recordemos que existen instancias distintas para esto, como el show() o el  

<br><br><br>

## Parte 2 — Transferencia a otra herramienta
**Piensa en tu pieza del Apply: si la quisieras recrear en Unity (o TouchDesigner, o Blender), ¿Qué se mantendría igual y qué cambiaría? ¿Qué partes de tu diseño son independientes de la herramienta?**

R// La estructura y logica seria similar por no decir que seria la misma, ya los metodos tecnicos para generar el mismo proyecto variarian dependiendo la plataforma.
Lo que no cambia al pasar de p5.js a Unity, TouchDesigner o Blender es la lógica conceptual del sistema:

El modelo de partículas la idea de que existen entidades con estado (posición, velocidad, vida, etc.) sigue siendo exactamente la misma. Otro elemento logico claro seria  l ciclo de vida:Crear → actualizar → destruir partículas es independiente del lenguaje o motor.
Por otro lado Las reglas de comportamiento: Cómo se mueven, cómo responden a fuerzas, cómo interactúan como por eEjemplo seria gravedad, ruido, atracción, repulsión.
La estructura del algoritmo:
El clásico esquema:
Inicializar → Actualizar en cada frame → Dibujar / representar
y finalemknte se mantendria bajo la misma logica la separación de responsabilidades

En conclusion y reiterando y confirmando lo dicho inicialmente, La lógica, las reglas y el diseño del sistema son independientes de la herramienta.



Si quisiera recrear el comportamiento de un sketch de p5js, es decir java script en Unity (o TouchDesigner, o Blender), ¿Qué se mantendría igual y qué cambiaría? ¿Qué partes de tu diseño son independientes de la herramienta?
