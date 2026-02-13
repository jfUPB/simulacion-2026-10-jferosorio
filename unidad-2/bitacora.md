# Unidad 2

VECTORES https://natureofcode.com/vectors/

https://juanferfranco.github.io/simulacion-2026-10/units/unit2/

https://www.youtube.com/watch?v=vTJWByS3Pi4

## Bitácora de proceso de aprendizaje


Un vector (posicion) + otro vector
La posicion anterior mas una velocidad que varia a travez del tiempo



X1=X0 + V DeltaT


V1 = V0 + A DeltaT
(velocidad en un punto es igual o aproximado a la velocidad anterior + la aceleracion en una variacion de tiempo(esta ña definimos con arte generativo))

Podemos hacer que la Aceleracion varie con un Gaussian.


*Integracion de Euler - Semi implicit (es la mas usada)*


Nosotros primero calculamos la velocidad y luego calculamos la posicion.

**Verlet integration** 


Cuando interactuo algo por delta de Time,



### 😎 Actividad 8


Aceleración constante.
Partiendo de; https://editor.p5js.org/natureofcode/sketches/4GSialOpQw

Relizamos algunos cambios con tal de jugar con el codigo, la finalidad era invertir la direccion del vector y que se generara mayor aceleracion y velocidad limite, tambien bajamos el tamaño del circulo, quedando asi:
```
class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector();
    this.acceleration = createVector(0.1, -0.1); //Cambiamos la direccion del vector de la aceleracion, 
    this.topSpeed = 100; //Cambiamos limite de velocidad para que alcance mas velocidad.
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    strokeWeight(2); //Tamaño del borde de lo que mostremos, en este caso circulo
    fill(127); //Cambiamos el color
    circle(this.position.x, this.position.y, 28); //Cambiamos el tamaño del circulo
  }
                    // Esta funcion indica que si la posicion de del circulo llega a tocar algun valor limite del canvas, ya sea altura o ancho, reinicie su posicion. Si la posicion en X es mayor a al ancho, entonces reinicia su posicion al punto de inicio. Asi mismo si la posicion en Y es mayor al alto del canvas, reinicia su posicion.
  checkEdges() {
    if (this.position.x > width) {
      this.position.x = 0;
    } else if (this.position.x < 0) {
      this.position.x = width;
    }

    if (this.position.y > height) {
      this.position.y = 0;
    } else if (this.position.y < 0) {
      this.position.y = height;
    }
  }
}
```
 Con esto creamos un efecto de caida en diagonal.


<br><br>
Aceleración aleatoria.
Partiendo de; https://editor.p5js.org/natureofcode/sketches/w9DU8ccWMf
```

// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

class Mover{
  constructor(){
    this.position = createVector(width/2,height/2);
    this.velocity = createVector();
    this.acceleration = createVector();
    this.topSpeed = 5;
  }

  update() {
    // The random2D() function returns a unit vector pointing in a random direction.
    this.acceleration = p5.Vector.random2D();
    this.acceleration.mult(random(2));

    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 48);
  }

  checkEdges() {

    if (this.position.x > width) {
      this.position.x = 0;
    }
    else if (this.position.x < 0) {
      this.position.x = width;
    }

    if (this.position.y > height) {
      this.position.y = 0;
    }
    else if (this.position.y < 0) {
      this.position.y = height;
    }
  }

}
```
<br><br>
Aceleración hacia el mouse.
Partiendo de; https://editor.p5js.org/natureofcode/sketches/gYJHm1EFL
```

```

## 👌MOTION 101.


Porque con tres vectores puedes simular:
gravedad
atracción
repulsión
ruido
comportamientos orgánicos
movimiento “inteligente”
Etc.

Sin motores físicos complejos.

Tener en cuenta; Hay que limitar la velocidad si no todo se va a la vrga, 

## Bitácora de aplicación 


Se busca generar una obra que simule el viaje a travez del espacio, mas especificamente la entrada a "hyper espacio", estos fragmentos donde un elemento viaja a valocidades mayores a la de la luz, tomando como referencias obras del Scifi como Star Wars, Halo o Star Trek. Se extenderan un primer grupo de estrellas simulando la entrada al HyperSpace y poteriormente habran una serie de lineas que simularan el paso de estrellas a una gran velocidad.
El color y el grosor del rastro se parametrizan a partir de variables dinámicas como la velocidad y el tiempo, reforzando visualmente la sensación de energía y ruptura del espacio-tiempo. Habran entonces puntos (lineas) pequenas que simularan las estrellas, estas seran en mayor numero, y otros objetos mas grandes en otros colores como lo puede ser el amarillo, apareceran en menos medida simulando estrellas d emayor tamano o planetas.

Se busca aplicar el principio del Motion 101, objetos que cambian su posición, velocidad y aceleración a lo largo del tiempo, aqui lo aplicamos iniciando con una entrada relativamente lenta y luego puntos empujados que cambian su direccion y aceleracion. n este proyecto se aplica Motion 101 porque el movimiento de cada estrella se construye a partir de la relación fundamental entre posición y velocidad, y su evolución en el tiempo, en lugar de mover los objetos de forma directa o “teletransportada”

Cada estrella tiene una posición (this.position) representada como un vector y una velocidad definida por una dirección (this.velocity, obtenida a partir de un ángulo aleatorio) y una magnitud (this.speed).

Link al proyecto: https://editor.p5js.org/jferosorio/sketches/m1txzvDLI

```
let stars = [];
let totalStars = 1000;

function setup() {
  createCanvas(800, 600);
  
  
  for (let i = 0; i < totalStars; i++) {
    stars.push(new Star());
  }
}

function draw() {
  background(0, 30);

  for (let star of stars) {
    star.update();
    star.checkEdges();
    star.show();
  }

}

class Star {
  constructor() {
    this.reset();
  }
  
reset() {
  this.position = createVector(width / 2, height / 2);

  // Guardaremos la posicion previa, esto nos sirve para luego crear una Line que conecte con la nueva posicion y crear el efecto de degradado
  this.prevPosition = this.position.copy();

  let angle = random(TWO_PI); // devuelve un dato aleatorio en 2π radianes, es decir 360 grados.
  this.velocity = p5.Vector.fromAngle(angle);
  this.speed = random(0.1, 5); //Creamos una velocidad aleatoria entre un rango de 0.1 y 5, esto ayuda a crear la sensacion de tener estrellas mas lejor y otras mas cerca.


  }

 update() {
  // Aqui se aplica escencialmene Motion 101
  this.prevPosition = this.position.copy();

  let step = p5.Vector.mult(this.velocity, this.speed);
  this.position.add(step);
// agregamos un vector de aceleracion al la posicion de un elemento.
  this.speed *= 1.01;
    
  }

  
    show() {
  stroke('#16A8EB');
  strokeWeight(0.9);
      
  

  //Aqui creamos una linea entre la posicion actual y la anterior que guardamos.
  line(
    this.prevPosition.x,
    this.prevPosition.y,
    this.position.x,
    this.position.y);


  }

  checkEdges() {
    if (
      this.position.x < 0 || 
      this.position.x > width ||
      this.position.y < 0 || 
      this.position.y > height
    ) {
      // Si sale del canvas reinicia la posicion
      this.reset();
    }
  }
}
```



<img width="774" height="574" alt="image" src="https://github.com/user-attachments/assets/69d98348-5e0b-4b2d-887d-884635e81397" />
<img width="778" height="579" alt="image" src="https://github.com/user-attachments/assets/e34bc76e-e53f-4976-ab35-25783b20bc38" />

<img width="780" height="573" alt="image" src="https://github.com/user-attachments/assets/783e087b-7ac4-4f20-97ed-cc3900517e1d" />
<img width="779" height="577" alt="image" src="https://github.com/user-attachments/assets/ffd9f4fb-11ed-462b-870c-f2ce71c7a782" />



Se crea una variacion del proyecto, la cual consta de ubicar el punto del reinicio de las estrellas en la posicion del mouse, y rebajando el numero de estrellas

Link al proyecto https://editor.p5js.org/jferosorio/sketches/HIwUkCOqw

<img width="776" height="575" alt="image" src="https://github.com/user-attachments/assets/8902df1b-a7d6-46fd-9d2c-223b087a3c20" />


## Bitácora de reflexión


Revisando las obras e ideas de Jared y Jeffrey, observamos que tras de las iniciativas generativas, se procura simular o buscar replicar el comportamiento natural. 

Para nuestro proyecto simularemos el elemento mas basico de las obras de los autores mencionados, en este caso la atraccion. Una fuerza que busca juntar elementos bajo determinado parametro, puede ser la busqueda de un elemento en busca de otro, la reunion de varios elementos con condiciones similares, etc. En este caso generamos 5 tipos de particulas, diferenciadas unicamente por su color, el numero de estas particulas puede ser variable. La idea es que particulas del mismo color se vean atraidas entre si, replicando lo que puede ser la seleccion natural, o **Hemofilia**. Fenomenos visibles en areas del conocimiento como la biologia, la ecologia, o incluso en la actualidad humana en las redes sociales.

**Link del proyecto** https://editor.p5js.org/jferosorio/sketches/roJ5PVXnS

<img width="777" height="572" alt="image" src="https://github.com/user-attachments/assets/a7fb587e-1ac8-43ad-8188-fc90683ee700" />

<img width="773" height="568" alt="image" src="https://github.com/user-attachments/assets/42efe06a-419a-4bfb-83ed-203d0ae8de6d" />

<img width="775" height="572" alt="image" src="https://github.com/user-attachments/assets/704e63b3-c4d8-4676-9b2d-acd2978e2b02" />

<img width="778" height="572" alt="image" src="https://github.com/user-attachments/assets/fa63d22c-3852-4387-ad5b-977f6ee75a2e" />






