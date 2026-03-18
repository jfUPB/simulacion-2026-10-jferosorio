# Unidad 5
## Bitácora de proceso de aprendizaje

Podemos crear un sistema de particulas
Podemos crear un sistema de sistemas de particulas, clickear el canvas y generar el sistema de particulas

Herencia y poliformismo. El comportamiento se solicita en su comportamiento a partir de encapsular sus caracteristicas.



### Actividad 1 Anatomía de una partícula
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

¿Quién crea las partículas? ¿En qué momento?
¿Quién decide cuándo eliminar una partícula del array?
¿Por qué se recorre el array en orden inverso para eliminar? ¿Qué pasaría si no se hiciera así?
Si no eliminaras nunca las partículas, ¿Qué pasaría con la memoria y el rendimiento? Haz el experimento: comenta la línea que elimina y observa el frame rate.


**Capa de visualización:**

¿Qué elementos visuales usa para representar una partícula?
¿Cómo se conecta el “tiempo de vida” con la apariencia visual?
Si quisieras cambiar la representación visual (por ejemplo, usar líneas en vez de círculos), ¿Qué cambiarías y qué NO cambiarías?





### Actividad 4; Fuerzas y particulas


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

## Bitácora de reflexión
