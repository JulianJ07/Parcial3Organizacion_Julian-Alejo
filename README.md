# PLANEACION JUEGO - Pacman Futbolero

## Desarrollado por:
Julian Jimenez,
Alejandro Cifuentes.

---
## Proposito de esta entrega

Esta version es una entrega estructural para Nand2Tetris en Jack. El objetivo no es entregar todavia el juego completo, sino demostrar que ya existe una base funcional con:

- un tablero visible dibujado con la API `Screen`;
- un personaje implementado como objeto;
- movimiento con teclado usando `Keyboard.keyPressed()`;
- cambio de velocidad del personaje;
- puntos coleccionables dentro del mapa;
- un impulsor de velocidad que aumenta temporalmente la velocidad del jugador;
- estructura modular con clases separadas.

La version completa del juego se desarrollara en una entrega posterior. En esa entrega final se agregaran rivales, poder para comer rivales, portales, colisiones avanzadas y condiciones completas de victoria o derrota.
<p align="center">
  <img 
    src="https://github.com/user-attachments/assets/d2d1b0c3-ce9f-4646-a450-03df833cc0de"
    alt="Imagen del proyecto"
    width="700"
  />
</p>


## Como ejecutar

1. Abre el VM Emulator de Nand2Tetris:
   `C:\Users\Julian\Downloads\nand2tetris\nand2tetris\tools\VMEmulator.bat`

2. Selecciona:
   `File > Load Program`

3. Carga esta carpeta:
   `C:\Users\Julian\Documents\Codex\2026-04-28\PLANEACION JUEGO`

4. Cambia `Animate` a:
   `No animation`

5. Sube la velocidad del emulador hacia `Fast`.

6. Ejecuta con el boton `>>`.

## Controles

- Flecha izquierda: mover a la izquierda.
- Flecha arriba: mover hacia arriba.
- Flecha derecha: mover a la derecha.
- Flecha abajo: mover hacia abajo.
- Tecla `1`: velocidad lenta.
- Tecla `2`: velocidad normal.
- Tecla `3`: velocidad rapida.
- Tecla `R`: reiniciar el juego.
- `ESC`: salir.

El jugador recoge automaticamente los puntos al pasar por encima de ellos. Si recoge el impulsor de velocidad, la velocidad aumenta durante un tiempo corto y luego vuelve al nivel elegido con las teclas `1`, `2` o `3`. Con `R` se reinicia el tablero, el puntaje, el impulsor y la posicion inicial del jugador.

## Estructura de clases

`Main.jack` es el punto de entrada. Crea el objeto `Game`, ejecuta el ciclo principal y libera memoria al terminar.

`Game.jack` controla el flujo del programa. Lee el teclado, aplica el movimiento, permite cambiar la velocidad, suma el puntaje de los puntos recogidos, activa el impulsor temporal de velocidad y reinicia la partida cuando se presiona `R`.

`Board.jack` representa el tablero. Define las dimensiones de la cuadricula, convierte filas y columnas a coordenadas de pantalla, valida paredes con `canEnter()`, guarda los puntos e impulsores en un arreglo `Array` y dibuja el mapa usando `Screen.drawRectangle()`.

`Player.jack` representa al futbolista. Guarda su fila y columna como `field`, valida si puede moverse y redibuja solamente la celda anterior y la nueva para evitar parpadeo innecesario.

## Relacion con la rubrica

### Graficos con Screen

El tablero completo se dibuja con `Screen.drawRectangle()`. Cada celda tiene un tamano fijo de 10 pixeles, con paredes y caminos diferenciados visualmente. Los puntos coleccionables y el impulsor tambien se dibujan con la API `Screen`, sin depender de imagenes externas. Esto cumple el requisito de mostrar un tablero coherente y visible.

### Gestion de fichas con OOP

El personaje no esta escrito como codigo suelto dentro de `Main`; esta encapsulado en la clase `Player`. El tablero tambien esta encapsulado en `Board`, incluyendo la informacion de paredes, puntos e impulsores. Esta separacion facilita agregar rivales, portales y colisiones en la entrega final.

### Input y movimiento

El juego usa `Keyboard.keyPressed()` dentro del ciclo principal. Las flechas mueven al futbolista, las teclas `1`, `2` y `3` cambian la velocidad base y la tecla `R` reinicia la partida. Cuando el jugador recoge el impulsor, `Game` reduce temporalmente la espera entre movimientos para que el personaje avance mas rapido. El movimiento no redibuja todo el tablero en cada paso, solo actualiza las celdas necesarias.

### Arquitectura en Jack

La estructura esta dividida en `Main`, `Game`, `Board` y `Player`. Los constructores inicializan los campos necesarios, `Board` usa `Array.new()` para guardar el estado de los objetos del mapa y los metodos `dispose()` liberan memoria con `Memory.deAlloc()` o `Array.dispose()`.

## Plan para la entrega final

1. Mejorar los objetos coleccionables:
   mantener puntos normales, agregar objetos especiales como conos, trofeos y balones de poder.

2. Mejorar el puntaje:
   cada objeto sumara una cantidad diferente de puntos y se mostrara una condicion clara de victoria.

3. Agregar rivales:
   se implementaran como objetos de una clase `Rival`, con posicion, dibujo y movimiento propio.

4. Agregar persecucion:
   los rivales buscaran al jugador usando rutas validas del laberinto, evitando paredes.

5. Agregar poder temporal:
   al recoger un balon, el jugador podra derrotar rivales durante unos segundos.

6. Agregar colisiones:
   si un rival toca al jugador sin poder activo, se termina la partida.

7. Agregar condicion de victoria:
   el jugador gana al recoger todos los objetos del tablero.

8. Agregar portales:
   se planearan como celdas especiales que transportan al jugador de un punto del mapa a otro. No estan implementados en esta entrega estructural.

9. Optimizar rendimiento:
   se evitara redibujar todo el mapa en cada ciclo. Solo se actualizaran las celdas que cambien.

## Conclusion

Esta entrega deja lista la base estructural de Pacman Futbolero en Jack. El proyecto ya muestra un tablero funcional con `Screen`, un futbolista encapsulado como objeto, movimiento controlado con `Keyboard.keyPressed()`, puntos coleccionables, impulsor de velocidad, reinicio de partida y una arquitectura separada en clases. Con esta base, la entrega final podra crecer de forma ordenada agregando rivales, persecucion, poderes, portales planeados, colisiones y condiciones completas de victoria o derrota.

El codigo cumple el enfoque principal de la rubrica porque demuestra uso de API grafica, manejo de input, organizacion orientada a objetos y actualizacion controlada de pantalla para evitar redibujos innecesarios.
