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



## Bitácora de aplicación 



## Bitácora de reflexión


