# Unidad 1

## Bitácora de proceso de aprendizaje

El artista imagina la herramienta que soluciona el problema, imagina la herramienta que crea. Es como una relacion padre e hijo, el padre ofrece conocimientos, guias y valores, el hijo acoge esas herramientas pero no se puede determinar precisamente su comportamiento.
La aleatoriedad es una prueba y error super rápido. Busca las vías (más óptimas) para resolver un problema o para crear.

La aleatoriedad como la bandera de la creación.
Humanizar el resultado de la máquina.
La aleatoriedad como las diferentes formas de interpretación

Crear productos “vivos”

"Es las creativa la tecnologia que el ser humano?"

Piensa y describe en una sola frase y en tus propias palabras cómo la aleatoriedad influye en el arte generativo.
La aletoriedad es la puerta a la infinidad de resultados esperados y no esperados 
La aletoriedad como la variable de variables

Tomando el codigo de https://editor.p5js.org/jferosorio/sketches/_M9jYgboV

// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker(); //walker contiene la direccion de New Walker que es un espacio en la memoria
  background(200);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}


La distribucion de probabilidad de uniforme, todos los numeros de la secuencia tienen la misma probabilidad de salir.


### Actividad 3

La distribucion es uniforme y la no uniforme. 
Cuando el comportamiento del experimento en UNIFORME, se entiende que todos los valores posibles tienen una probabiilidad similar de seleccionarse, por tanto se entiende que graficamente no se observara una campana si no una linea continua.

Cuando el comportamiento de un experimento es NO UNIFORME, se entiende que hay valores que tienen las probabilidad de ser seleccionados, estos datos se les conoce como la media, graficamente, entre menos sea el rango o DESVIACION ESTANDAR esta campana de Gauss se vuelve menos ancha y el pico es mas notorio.


Podemos modificar nuestra distribucion de probabilidad 
Si queremos que nos salga un resultado esperado si alterar la forma de seleccino podemos modificar lo que sera seleccionado, ejemplo los gatos de colores


### Actividad 4

### Actividad 5
SALTOS DE LEVY

## Bitácora de aplicación 



## Bitácora de reflexión


