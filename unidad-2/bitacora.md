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


Se busca generar una obra que simule el viaje a travez del espacio, mas especificamente la entrada a "hyper espacio", estos fragmentos donde un elemento viaja a valocidades mayores a la de la luz, tomando como referencias obras del Scifi como Star Wars, Halo o Star Trek. 
El color y el grosor del rastro se parametrizan a partir de variables dinámicas como la velocidad y el tiempo, reforzando visualmente la sensación de energía y ruptura del espacio-tiempo.

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

Link al proyecto: https://editor.p5js.org/jferosorio/sketches/m1txzvDLI

<img width="774" height="574" alt="image" src="https://github.com/user-attachments/assets/69d98348-5e0b-4b2d-887d-884635e81397" />
<img width="778" height="579" alt="image" src="https://github.com/user-attachments/assets/e34bc76e-e53f-4976-ab35-25783b20bc38" />


## Bitácora de reflexión



