# Unidad 3


<img width="1720" height="813" alt="image" src="https://github.com/user-attachments/assets/5eb73342-7f7a-46bc-b15d-e228fbd1c95a" />
<img width="1312" height="654" alt="image" src="https://github.com/user-attachments/assets/88e98f98-09e3-4d42-b259-d7da575c528e" />



## Bitácora de proceso de aprendizaje

https://juanferfranco.github.io/simulacion-2026-10/units/unit3/
https://roberthodgin.com/

Trabajo de modular, diferentes metodos.

hasta ahora tenemos
```
class Mover {
  constructor() {
    this.position = createVector();
    this.velocity = createVector();
    this.acceleration = createVector();
  }
}
```


Vamos a intereactuar por medio de la palicacion de fuerzas.
Sumaremos todas las fuerzas que tenemos y la dividiremos entre Masa, este sera un parametro mas.

Ahora agregaremos una fuerza con nuevo motodo **mover.applyForce(wind);**

```
applyForce(force) {
  // Recuerdo, estamos asumiendo que la masa es 1, entonces no es necesario dividir la fuerza por la masa.
  this.acceleration.add(force);
}
```

Ventajas de locarl; 1. Trabajar en mejor editos y con iA.caht


### 👌Actividad 3
1. Inventar la fuerza, puede ser un perlin, un random, la conectamos a la narrativa.
2. Modelar una fuerza existente, una de la vida real, puede ser friccion resistencia o gravedad


FRICCION https://editor.p5js.org/jferosorio/sketches/XM_Qq22XN
<img width="581" height="379" alt="image" src="https://github.com/user-attachments/assets/28b99b52-2ba3-44e7-83bd-2fadc4596c23" />


FLUIDO https://editor.p5js.org/jferosorio/sketches/X7fzw0Lyb
<img width="587" height="371" alt="image" src="https://github.com/user-attachments/assets/7ce5d3a7-fff7-43d3-b968-3e7d515bc991" />

GRAVEDAD https://editor.p5js.org/jferosorio/sketches/n12Mt1y0D
<img width="472" height="253" alt="image" src="https://github.com/user-attachments/assets/fcae252f-6893-41fc-a8a6-9ac2504d0ca8" />




## Bitácora de aplicación 






## Bitácora de reflexión

