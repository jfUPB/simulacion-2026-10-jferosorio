
<img width="986" height="237" alt="image" src="https://github.com/user-attachments/assets/2234e071-34be-4b7c-a6b6-c7a2d20bad25" />

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

Inspirado en el viaje de Dante a travez de la divina comedia me gustaria plasmar "ciclo de vida" en el proceso de redencion del paso de la humanidad a la eternidad, asi como el paso por los circulos del infieno, el trayecto del purgatorio y la llegada al paraiso. Mi particula principal realizar este viaje mencionado, iniciando en forma de estrella y manchada y con una estela a fin de simular , a medida que avanza por la experiencia esta se ira trasformando hasta convertirse en una esfera de color claro. L


Otra idea
Ciclo del agua. Inicia con una gota que sale de la parte superior del canvas que simula el cielo, cae y pasa por el ciclo del agua y termina subiendo a la parte superior del canvas y muere.

Para tener en cuenta
Podemos generar el comportamiento en el show(), de tal manera que cierto rango del tiempoi de vida de la partidcula tenga ciertas caracteristicas, que de 255 a 150 tal cosa, de 150 a 100 de trasforma y de 100 a 0 muere y pasa tal cosa

El run()

en for() realiza el repaso de las posiciones d elas particulas al reves por el -1 por el tema explicado
<img width="1557" height="732" alt="image" src="https://github.com/user-attachments/assets/61d5ec46-ce03-4562-893f-41c49e71c092" />

<img width="803" height="301" alt="image" src="https://github.com/user-attachments/assets/30b3c3f6-7c7d-45fd-87c7-b87d13594729" />


## Bitácora de reflexión
