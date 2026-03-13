# Unidad 4

## Bitácora de proceso de aprendizaje

## 👌**Actividad 1**

<img width="1064" height="455" alt="image" src="https://github.com/user-attachments/assets/fc977d65-075d-4664-85d0-efee58f39029" />


Las obras de arte generativo de Memo Akten se caracterizan por mezclar arte, tecnología y ciencia de una forma muy natural. Gran parte de su trabajo se basa en el uso de algoritmos, inteligencia artificial y aprendizaje automático para generar imágenes y experiencias visuales que cambian constantemente. En lugar de crear una obra fija, Akten diseña sistemas que producen resultados impredecibles, muchas veces inspirados en procesos de la naturaleza como el movimiento de fluidos, partículas o formas orgánicas. Esto hace que sus obras tengan una estética muy dinámica, que parece viva o en constante transformación.

Además, muchas de sus piezas buscan que el espectador participe o reflexione sobre la relación entre los humanos y la tecnología. A través de instalaciones interactivas, visuales generativos y presentaciones audiovisuales en tiempo real, su trabajo explora cómo las máquinas pueden “percibir” el mundo y cómo esa percepción se diferencia de la humana. Más que solo crear imágenes llamativas, sus obras suelen plantear preguntas sobre la inteligencia artificial, la conciencia y la forma en que la tecnología está cambiando nuestra manera de entender la realidad.


## 👌**Actividad 2**

<img width="603" height="230" alt="image" src="https://github.com/user-attachments/assets/3c44d314-143f-4e8a-ac62-31aad32b6e7a" />

Revisando el fragmento;
```
  display() {
    let angle = this.velocity.heading();

    stroke(0);
    strokeWeight(2);
    fill(127);
    push();
    rectMode(CENTER);
    translate(this.position.x, this.position.y);
    rotate(angle);
    rect(0, 0, 30, 10);

    pop();
  }
```

1. El marco Motion 101 describe el movimiento usando tres elementos principales:

posición (position)
velocidad (velocity)
aceleración (acceleration)

Aquí no se calcula el movimiento, sino la forma en que el objeto se dibuja según su velocidad.
```
let angle = this.velocity.heading();
```
El objeto rota según la dirección en la que se está moviendo.


2. heading() es una función de los vectores y esta calcula el ángulo del vector respecto al eje X.


3. Push y pop guardan y restauran el estado del sistema de dibujo.

Incluye:

traslación
rotación
escala
estilos

push()
Guarda el estado actual.

pop()
Vuelve al estado anterior.

EN el CODIGO Significa que solo ese rectángulo se dibuja rotado.

rectMode(CENTER), Es como si definieramos el punto de pivote del rectangulo Si no usas CENTER rota desde una esquina, pues es el punto de origen naturalmente del rectangulo. Si se usa  CENTER rota desde su centro.

Finalmente...
La Relación entre ángulo y vector de velocidad es el concepto más importante.
El vector de velocidad tiene:
dirección
magnitud

heading() extrae la dirección. Ese vector tiene un ángulo y finalmente el objeto se dibuja

<img width="821" height="583" alt="image" src="https://github.com/user-attachments/assets/0a56ed97-5952-4d9b-8ba6-12612ffbece5" />



## 👌**Actividad 3**  

**Crea una simulación de un vehículo que puedas conducir por la pantalla utilizando las teclas de flecha: la flecha izquierda acelera el vehículo hacia la izquierda, y la flecha derecha acelera hacia la derecha. El vehículo tendrá forma triangular y debe apuntar en la dirección en la que se está moviendo actualmente**



Link al proyecto https://editor.p5js.org/jferosorio/sketches/wmkgGy9Wc
```
let vehicle;

function setup() {
  createCanvas(500, 400);
  vehicle = new Vehicle(width/2, height/2);
}

function draw() {
  background(240);

  vehicle.update();
  vehicle.edges();
  vehicle.show();
}

class Vehicle {

  constructor(x,y){
    this.position = createVector(x,y);
    this.velocity = createVector(0,0);
    this.acceleration = createVector(0,0);

    this.maxSpeed = 5;
  }

  applyForce(force){
    this.acceleration.add(force);
  }

  update(){

    // control con flechas
    if (keyIsDown(LEFT_ARROW)){
      this.applyForce(createVector(-0.1,0));
    }

    if (keyIsDown(RIGHT_ARROW)){
      this.applyForce(createVector(0.1,0));
    }

    // MOTION 101
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.maxSpeed);
    this.position.add(this.velocity);

    this.acceleration.mult(0);
  }

  edges(){
    if (this.position.x > width) this.position.x = 0;
    if (this.position.x < 0) this.position.x = width;
  }

  show(){

    // ángulo según dirección de movimiento
    let angle = this.velocity.heading();

    push();
    translate(this.position.x, this.position.y);
    rotate(angle);

    fill(0,150,255);
    stroke(0);

    //vehículo
    triangle(-15,-10,-15,10,20,0);

    pop();
  }

}
```
  



## 👌**Actividad 4**

1.Cuando se quieren aplicar varias fuerzas en un mismo frame (por ejemplo gravedad, viento, fricción o atracción), es necesario reiniciar la aceleración después de actualizar el movimiento.

Por eso se agrega la línea:this.acceleration.mult(0);

Quedando asi
```
// MOTION 101
this.velocity.add(this.acceleration);
this.position.add(this.velocity);

// reiniciar aceleración
this.acceleration.mult(0);
```

2. Link con atractor cambiado de color https://editor.p5js.org/jferosorio/sketches/2qaDbK0xk 

3. 




## 👌**Actividad 5 oordenadas polares**




## 👌**Actividad 6; Funciones sinusoides**
## 👌**Actividad 7 ; Repaso conceptos**
## 👌**Actividad 8; Ondas**

## 👌**Actividad 8; Resortes**

## 👌**Actividad 8; Pendulos**






## Bitácora de aplicación 

https://editor.p5js.org/jferosorio/sketches/cBQxiNxnE
<img width="586" height="385" alt="image" src="https://github.com/user-attachments/assets/1dbf3452-b58c-4f25-baa1-6564676186ed" />

https://editor.p5js.org/jferosorio/sketches/fhoVUg1Hn
<img width="593" height="386" alt="image" src="https://github.com/user-attachments/assets/38947981-f82d-4bb6-a6a3-f4e84abb79a4" />


## Bitácora de reflexión





