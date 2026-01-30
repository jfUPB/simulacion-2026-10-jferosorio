

# Unidad 1

Link al curso se simulaccion https://juanferfranco.github.io/simulacion-2026-10/units/intro/

## Bitácora de proceso de aprendizaje

*El artista imagina la herramienta que soluciona el problema, imagina la herramienta que crea. Es como una relacion padre e hijo, el padre ofrece conocimientos, guias y valores, el hijo acoge esas herramientas pero no se puede determinar precisamente su comportamiento.*



Crear productos “vivos”

"Es las creativa la tecnologia que el ser humano?"

<br><br>

### 😎Actividad 01
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

<br><br>

### 😎 Actividad 02 - Caminatas aleatorias
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
El Walker nace en el centro del lienzo 

<br><br>

### 😎Actividad 3
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


**Condigo que muestra 3 tipos de distribuciones de probabilidad**
<img width="919" height="295" alt="image" src="https://github.com/user-attachments/assets/dca39eff-abce-441f-a29c-e9facc43a271" />

```
function setup() {
  createCanvas(640, 240);
  background(200);
}

function draw() {
  //{!1} A normal distribution with mean 320 and standard deviation 60
  let x = randomGaussian(320, 120); //Aqui se define la media y la desviacion de estandar
  // no hay let y pr lo que se pondra en la mitad.
  let sqrColor= randomGaussian(2, 20)
  noStroke();
  fill(sqrColor, 2);
  square(x, 120, 16);
{
let x = randomGaussian(320, 120);
  let y =70

  noStroke();
  fill(0, 10);
  square(x, y, 16);
  {
  let x = randomGaussian(320, 10);
  let y =90

  noStroke();
  fill(0, 10);
  square(x, y, 16);

}

}}
```


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

<br><br>

### 😎Actividad 4
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

<br><br>


### 😎Actividad 5 - SALTOS DE LEVY
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


<br><br>


### 😎Actividad 6 - Ruido perlin
```
Crea un nuevo sketch en p5.js donde los visualices.
Explica el concepto qué resultados esberabas obtener.
Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
```

<img width="1189" height="378" alt="image" src="https://github.com/user-attachments/assets/7fa8f3f1-3a62-4aa8-94a9-904b5f1b0ffe" />

Al lado izquierdo aplicacion de ruido perlin, lo que acota el espectro de opciones, es decir que controlamos su desviacion estandar. A la derecha un grafico con ruido normal, se ven como los resultados son mas volatiles, esto pues su desviacion estandar no esta controlada.

<br><br>


## Bitácora de aplicación 

### 😎Actividad 7 
```
Un texto donde expliques el concepto de obra generativa.
Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
```
Elegir 3 conceptos 

Camino del artista, va descubriendo en el camino
El diseñador primero planea

💡 Se buscará crear una experiencia en la que segun la posicion del mouse en el eje X se reciba un determinado comportamiento de un **RandomWalker**, si el mouse se encuentra hacia la izquierda obtendremos una caminata tranquila y con menos **saltos de Levy** (es decir que reduciremos su **distribucion normal, es decir aplicaremos un randomGauss**) y su recorrido obtendra un color azul (frio), si el mouse se encuentra mas hacia la derecha el movimiento sera mas erratico (**aplicaremos una distribucion normal unifrome**), habran mas saltos y el color torna rojo (calido). Para ello:

```
let walker;

function setup() {
  createCanvas(640, 240);
  background(200);
  walker = new Walker();
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

  step() {
    // Normalizamos la posición del mouse (0 izquierda, 1 derecha). Constrain nos permite limitar los valores que queremos que el elemento mouseX/anchoCanvas
que es la posicion del mouse se mantenga entre 0 (el inicio del camvas y 1, que es el final).
Recordar que estos elementos nos extienden valores PORCENTUALES
    let m = constrain(mouseX / width, 0, 1);

    // Velocidad y erraticidad
    let steps = int(lerp(1, 5, m)); // más pasos si el mouse va a la derecha, con lerp, establecemos un rango en el que, en este caso m, elije segun cierto dato
-En el caso concreto- Aqui indicamos el rango entre 1 y 5, y m lo indicamos anteriormente que sera un porcentage determinado entre la posicion del mouse/anchoCanvas.
Usamos int para que convierta el resultado dado en un entero
    let levyChance = lerp(0.05, 0.15, m); // más saltos de Lévy a la derecha. Aqui lerp funciona de la misma manera, estableceun rango,
en este caso 5% y 15% y segun el dato de m este tiende mas hacia un extremo del rango o el otro

    for (let i = 0; i < steps; i++) {
      let stepSize = 1;

      // Saltos de Lévy
      if (random(1) < levyChance) {
        stepSize = pow(random(1), -2) * 2;
        stepSize = constrain(stepSize, 1, 40);
      }

      let angle = random(TWO_PI);
      this.x += cos(angle) * stepSize;
      this.y += sin(angle) * stepSize;
    }
  //Aqui limitaremos que el resultado del salto y movimientos se queden dentro del Canvas parametrizando el rango en el que pueden darse los resultados nuevamente con CONSTRAIN, en este caso lo parametrizamos entre 0 y la medida del ancho o alto segun corresponda restado  - 1 para evitar algunos errores.
    this.x = constrain(this.x, 0, width - 320);
    this.y = constrain(this.y, 0, height - 120);
  }

  show() {
    let m = constrain(mouseX / width, 0, 1);

    // Interpolación de color
    let cold = color(50, 100, 255, 900);   // azul
    let warm = color(255, 60, 60, 900);   // rojo
    let c = lerpColor(cold, warm, m);

    stroke(c);
    circle(this.x, this.y, 2);
  }
}

```
Mouse en posicion hacia la izquierda con caminata mas tranquila
<img width="634" height="235" alt="Captura de pantalla 2026-01-28 110147" src="https://github.com/user-attachments/assets/bccbbebd-0fa6-4bea-ac3e-a26c33726335" />

Mouse en posicion hacia la derecha con caminata mas erratica
<img width="631" height="230" alt="Captura de pantalla 2026-01-28 110209" src="https://github.com/user-attachments/assets/d57b84a8-98a4-450d-89fe-bba6f264befb" />

Mouse centrado con caminata intermedia  
<img width="638" height="229" alt="Captura de pantalla 2026-01-28 110226" src="https://github.com/user-attachments/assets/604af6ba-d423-40f8-945e-ad5f4b1eb239" />

---
**link del proyecto**
https://editor.p5js.org/jferosorio/sketches/7nCEU2RVMs
---
Conceptos aplicados, caminitas aletorias, saltos de levy, ruido de perlin, distribucion normal, 

Para repasar sobre constrain; https://p5js.org/es/reference/p5/constrain/
Para repasar sobre lerp; https://p5js.org/reference/p5/lerp/


<br><br>



## Bitácora de reflexión


```
Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?
Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?
¿Cuál es el papel de la aleatoriedad en el arte generativo? Menciona al menos dos funciones distintas que cumple
Piensa en tu obra final (Actividad 07). Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.
¿Qué es un “paseo” o “caminata” (walk) en el contexto de la simulación? ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?
```
🤔
### 1. Diferencia Random y Noise
Con random(), cada valor es impredecible y no tiene relación con el anterior. Esto produce resultados abruptos saltos bruscos.
 El Ruido Perlin da la apariencia de aleatoriedad, pero en realidad es una función continua: valores cercanos producen resultados similares. se genera transiciones suaves y orgánicas.*

### 2. Distribucion de propabilidad, ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?
Una distribución de probabilidad describe qué tan probable es que ocurran ciertos valores dentro de un conjunto de posibilidades, la caminata aletoria con distribucion normal sera mas erratica, mas inesperdad pues se tiene una gamma mas aplica de posibilidades y que tienen la misma propabilidad de ser elegidos, entonces si tenemos Walker que se mueva solo en el eje X y Y, tendremos que moverse a la izquierda, a la derecho ariba o abajo, tendran la misma posibilidad de suceder. Por otro lado la distribucion uniforme o gausseana indica que la aletoriedad tendra preferencia por ciertos datos determinados en un rango y por su normal, por ende seran elegidos de manera mas reiterativa datos cercanos, vistualmente se vera un movimiento mas suave, variable pero no brusco. Estos concepto sya los abordamos anteriormente en la bitacora cuando trajimos la siguiente captura;

<img width="1007" height="377" alt="image" src="https://github.com/user-attachments/assets/95072d45-d81b-44d1-86f2-2993f3baf769" />


### 3. EL papel de la aletoriedad en el arte generativo
Observamos que  aleatoriedad cumple roles clave, como introducir variación y evitar la repetición y tambien permite que cada ejecución de la obra sea distinta, aunque siga las mismas reglas. Por otro lado tal como lo mencionamos incialmente buscamos crear un producto vivo, "humanizamos la maquina" por lo que se puede decir que esta aletoriedad se busca simular comportamientos naturales.

### 4. Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.
Usamos random para establecer el elemento de la aletoriedad en nuestra caminata, esta aletoriedad la aplicamos de manera interactiva y variable segun la posicion de mouse en X, por lo que podemos decir que establecimos en el movimiento del mouse la capacidad de alterar la distribucion normal de las variables de nuestro proyecto, como la propabilidad de un salto de levy, y el color (solo entre azul y rojo).


### Que es un paseo o caminata, ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?
Una caminata en simulación es un proceso en el que un agente se mueve paso a paso, donde cada nueva posición depende de la anterior, generalmente con algún componente aleatorio. Una Lévy flight es un tipo especial de caminata que se caracteriza por pasos pequeños y de vez en cuando saltos muy largos.

---
🧠 *Bitácora desarrollada por Juan Fernando*  
🎮 *Ingeniería de Diseño de Entretenimiento Digital*









