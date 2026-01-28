

# Unidad 1

## Bitácora de proceso de aprendizaje

*El artista imagina la herramienta que soluciona el problema, imagina la herramienta que crea. Es como una relacion padre e hijo, el padre ofrece conocimientos, guias y valores, el hijo acoge esas herramientas pero no se puede determinar precisamente su comportamiento.*



Crear productos “vivos”

"Es las creativa la tecnologia que el ser humano?"

## 😎Actividad 01
```
Piensa y describe en una sola frase y en tus propias palabras cómo la aleatoriedad influye en el arte generativo.
```
🤔🤔*La aletoriedad es la puerta a la infinidad de resultados esperados y no esperados 
La aletoriedad como la variable de variables*
La aleatoriedad es una prueba y error super rápido. Busca las vías (más óptimas) para resolver un problema o para crear.
La aleatoriedad como la bandera de la creación.
Humanizar el resultado de la máquina.
La aleatoriedad como las diferentes formas de interpretación


Tomando el codigo de https://editor.p5js.org/jferosorio/sketches/_M9jYgboV



La distribucion de probabilidad de uniforme, todos los numeros de la secuencia tienen la misma probabilidad de salir.

## 😎 Actividad 02 - Caminatas aleatorias
```
Realiza el siguiente experimento y reporta los resultados en tu bitácora:

Modifica el código del ejemplo Example 0.1: A Traditional Random Walk.
Antes de ejecutar el código, escribe en tu bitácora qué esperas que suceda.
Ejecuta el código y escribe en tu bitácora qué sucedió realmente.
Ocurrió lo que esperabas? ¿Por qué crees que sí o por qué crees que no?
```

```
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
```

Cambiar createCanvas(640, 240) edita el tamano del lienzo ✅
Si ponemos un mismo dato en los else, solo tendra encuenta el primero ✅
Background es el color del lienzo 
El Walker nace en el centro del lienzo por 

## 😎Actividad 3
```
En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.
Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.
```
Existen distribucion  uniforme y  no uniforme. 
Cuando el comportamiento del experimento en UNIFORME, se entiende que todos los valores posibles tienen una probabiilidad similar de seleccionarse, por tanto se entiende que graficamente no se observara una campana si no una linea continua.

Cuando el comportamiento de un experimento es NO UNIFORME, se entiende que hay valores que tienen las probabilidad de ser seleccionados, estos datos se les conoce como la media, graficamente, entre menos sea el rango o DESVIACION ESTANDAR esta campana de Gauss se vuelve menos ancha y el pico es mas notorio.

Podemos modificar nuestra distribucion de probabilidad 
Si queremos que nos salga un resultado esperado si alterar la forma de seleccino podemos modificar lo que sera seleccionado, ejemplo los gatos de colores

Asi se logra modificar el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha. Editando el numero de posibilidades y limitando a que la eleccion que se escoja tienda al resultado que queremos
```
step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 0) {
      this.x--;
    } else if (choice == 0) {
      this.y++;
    } else {
      this.y--;
    }
```


## 😎Actividad 4

## 😎Actividad 5
SALTOS DE LEVY

## Bitácora de aplicación 



## Bitácora de reflexión


---
🧠 *Bitácora desarrollada por Juan Fernando*  
🎮 *Ingeniería de Diseño de Entretenimiento Digital*

