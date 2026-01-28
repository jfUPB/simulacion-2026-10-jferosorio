

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
```
Una vez has entendido el concepto de distribución normal, vas a pensar en una nueva manera de visualizarlo.

Crea un nuevo sketch en p5.js que represente una distribución normal.
Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
```
```
function setup() {
  createCanvas(640, 240);
  background(255);
}

function draw() {
  //{!1} A normal distribution with mean 320 and standard deviation 60
  let x = randomGaussian(320, 90);
  noStroke();
  fill(0, 10);
  circle(x, 120, 16);
}
```
<img width="597" height="237" alt="image" src="https://github.com/user-attachments/assets/6fc3d9ce-418e-4c71-b84d-c73226e3774d" />

*La distribucion normal hace referencia al rango en el que pueden ser sucedidas las posibilidades*


## 😎Actividad 5 - SALTOS DE LEVY
```
Crea un nuevo sketch en p5.js donde modifiques uno de los ejemplos anteriores y adiciones de Lévy flight.
Explica por qué usaste esta técnica y qué resultados esperabas obtener.
Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
```
variación de la caminata aleatoria
*cuanto más largo es el paso, menos probable es que sea elegido; cuanto más corto es el paso, más probable resulta.*
```
let r = random(1);
if (r < 0.01) {
  xstep = random(-100, 100);
  ystep = random(-100, 100);
A 1% chance of taking a large step

} else {
  xstep = random(-1, 1);
  ystep = random(-1, 1);
}
```
r < 0.01 indica que solo hay un 1% de probabilidad de realizar el salto. Si esta probabilidad se da, dara un salto aleatorio ubicado entre -100 puntos y 100 puntos en X, y  ubicado entre -100 puntos y 100 puntos en Y. De no cumplir esa condicion es decir que se escoja ese 1%, el movimiento sera aleatorio en un rango de 1 tanto en X y Y

## 😎Actividad 6 - Ruido perlin
```
Crea un nuevo sketch en p5.js donde los visualices.
Explica el concepto qué resultados esberabas obtener.
Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
```

## Bitácora de aplicación 


## 😎Actividad 7 - Ruido perlin
```
Un texto donde expliques el concepto de obra generativa.
Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
```



## Bitácora de reflexión


```
Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?
Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?
¿Cuál es el papel de la aleatoriedad en el arte generativo? Menciona al menos dos funciones distintas que cumple
Piensa en tu obra final (Actividad 07). Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.
¿Qué es un “paseo” o “caminata” (walk) en el contexto de la simulación? ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?
```
🤔
### Diferencia Random y Noise
Con random(), cada valor es impredecible y no tiene relación con el anterior. Esto produce resultados abruptos saltos bruscos.
 El Ruido Perlin da la apariencia de aleatoriedad, pero en realidad es una función continua: valores cercanos producen resultados similares. se genera transiciones suaves y orgánicas.*

### Distribucion de propabilidad
Una distribución de probabilidad describe qué tan probable es que ocurran ciertos valores dentro de un conjunto de posibilidades, 

### EL papel de la aletoriedad en el arte generativo
Observamos que  aleatoriedad cumple roles clave, como introducir variación y evitar la repetición y tambien permite que cada ejecución de la obra sea distinta, aunque siga las mismas reglas. Tal como lo mencionamos incialmente un producto vivo, "humanizamos la maquina" por lo que se puede decir que se busca simular comportamientos naturales

### Que es un paseo o caminata
Una caminata en simulación es un proceso en el que un agente se mueve paso a paso, donde cada nueva posición depende de la anterior, generalmente con algún componente aleatorio. Una Lévy flight es un tipo especial de caminata que se caracteriza por pasos pequeños y de vez en cuando saltos muy largos.
---
🧠 *Bitácora desarrollada por Juan Fernando*  
🎮 *Ingeniería de Diseño de Entretenimiento Digital*



