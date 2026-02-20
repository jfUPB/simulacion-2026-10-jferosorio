# Unidad 3

https://juanferfranco.github.io/simulacion-2026-10/units/unit3/


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

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 



## Bitácora de reflexión
