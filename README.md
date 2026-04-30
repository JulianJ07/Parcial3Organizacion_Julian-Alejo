# PLANEACION JUEGO - Pacman Futbolero

## Proposito de esta entrega

Esta version es una entrega estructural para Nand2Tetris en Jack. El objetivo no es entregar todavia el juego completo, sino demostrar que ya existe una base funcional con:

- un tablero visible dibujado con la API `Screen`;
- un personaje implementado como objeto;
- movimiento con teclado usando `Keyboard.keyPressed()`;
- cambio de velocidad del personaje;
- estructura modular con clases separadas.

La version completa del juego se desarrollara en una entrega posterior. En esa entrega final se agregaran rivales, objetos coleccionables, poder para comer rivales, puntaje, colisiones y condiciones de victoria o derrota.

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
- `ESC`: salir.

## Estructura de clases

`Main.jack` es el punto de entrada. Crea el objeto `Game`, ejecuta el ciclo principal y libera memoria al terminar.

`Game.jack` controla el flujo del programa. Lee el teclado, aplica el movimiento, permite cambiar la velocidad y mantiene el juego activo hasta que se presione `ESC`.

`Board.jack` representa el tablero. Define las dimensiones de la cuadricula, convierte filas y columnas a coordenadas de pantalla, valida paredes con `canEnter()` y dibuja el mapa usando `Screen.drawRectangle()`.

`Player.jack` representa al futbolista. Guarda su fila y columna como `field`, valida si puede moverse y redibuja solamente la celda anterior y la nueva para evitar parpadeo innecesario.

## Relacion con la rubrica

### Graficos con Screen

El tablero completo se dibuja con `Screen.drawRectangle()`. Cada celda tiene un tamano fijo de 10 pixeles, con paredes y caminos diferenciados visualmente. Esto cumple el requisito de mostrar un tablero coherente y visible.

### Gestion de fichas con OOP

El personaje no esta escrito como codigo suelto dentro de `Main`; esta encapsulado en la clase `Player`. El tablero tambien esta encapsulado en `Board`, lo que facilita agregar objetos, rivales y colisiones en la entrega final.

### Input y movimiento

El juego usa `Keyboard.keyPressed()` dentro del ciclo principal. Las flechas mueven al futbolista y las teclas `1`, `2` y `3` cambian la velocidad. El movimiento no redibuja todo el tablero en cada paso, solo actualiza las celdas necesarias.

### Arquitectura en Jack

La estructura esta dividida en `Main`, `Game`, `Board` y `Player`. Los constructores inicializan los campos necesarios y los metodos `dispose()` liberan memoria con `Memory.deAlloc()`.

## Plan para la entrega final

1. Agregar objetos coleccionables en el tablero:
   conos, trofeos y balones de poder.

2. Agregar puntaje:
   cada objeto sumara una cantidad diferente de puntos.

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

8. Optimizar rendimiento:
   se evitara redibujar todo el mapa en cada ciclo. Solo se actualizaran las celdas que cambien.

## Compilacion

Si modificas los archivos `.jack`, recompila la carpeta con:

`C:\Users\Julian\Downloads\nand2tetris\nand2tetris\tools\JackCompiler.bat "C:\Users\Julian\Documents\Codex\2026-04-28\PLANEACION JUEGO"`

