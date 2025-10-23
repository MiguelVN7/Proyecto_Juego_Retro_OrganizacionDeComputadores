# API Documentation - Breakout Game

## Main

### `function void main()`
Punto de entrada del programa. Crea una instancia de BreakoutGame y ejecuta el juego.

---

## BreakoutGame

### Constructor
- `constructor BreakoutGame new()`
  - Inicializa el juego
  - Crea paleta, pelota y bloques
  - Establece estado inicial

### Methods
- `method void run()`
  - Loop principal del juego
  - Procesa input del usuario
  - Actualiza estado del juego
  - Renderiza elementos

- `method void dispose()`
  - Libera memoria de todos los objetos

---

## Paddle

### Constructor
- `constructor Paddle new(int x, int y, int width, int height)`
  - `x`: Posición X inicial
  - `y`: Posición Y inicial
  - `width`: Ancho de la paleta
  - `height`: Alto de la paleta

### Methods
- `method void draw()`
  - Dibuja la paleta en su posición actual

- `method void moveLeft()`
  - Mueve la paleta hacia la izquierda

- `method void moveRight()`
  - Mueve la paleta hacia la derecha

- `method int getX()`
  - Retorna la posición X actual

- `method int getY()`
  - Retorna la posición Y actual

- `method int getWidth()`
  - Retorna el ancho de la paleta

- `method int getHeight()`
  - Retorna el alto de la paleta

- `method void dispose()`
  - Libera memoria

---

## Ball

### Constructor
- `constructor Ball new(int x, int y, int radius)`
  - `x`: Posición X inicial
  - `y`: Posición Y inicial
  - `radius`: Radio de la pelota

### Methods
- `method void draw()`
  - Dibuja la pelota en su posición actual

- `method void move()`
  - Actualiza la posición según la velocidad actual

- `method void bounceHorizontal()`
  - Invierte la velocidad horizontal (rebote izquierda/derecha)

- `method void bounceVertical()`
  - Invierte la velocidad vertical (rebote arriba/abajo)

- `method int getX()`
  - Retorna la posición X actual

- `method int getY()`
  - Retorna la posición Y actual

- `method int getRadius()`
  - Retorna el radio de la pelota

- `method void reset(int x, int y)`
  - Reinicia la pelota en la posición especificada

- `method void dispose()`
  - Libera memoria

---

## Block

### Constructor
- `constructor Block new(int x, int y, int width, int height, int points)`
  - `x`: Posición X
  - `y`: Posición Y
  - `width`: Ancho del bloque
  - `height`: Alto del bloque
  - `points`: Puntos otorgados al destruir

### Methods
- `method void draw()`
  - Dibuja el bloque si está activo

- `method void erase()`
  - Borra el bloque de la pantalla

- `method boolean isActive()`
  - Retorna true si el bloque no ha sido destruido

- `method void destroy()`
  - Marca el bloque como destruido

- `method int getX()`
  - Retorna la posición X

- `method int getY()`
  - Retorna la posición Y

- `method int getWidth()`
  - Retorna el ancho

- `method int getHeight()`
  - Retorna el alto

- `method int getPoints()`
  - Retorna los puntos que otorga

- `method void dispose()`
  - Libera memoria

---

## BlockGrid

### Constructor
- `constructor BlockGrid new(int rows, int cols)`
  - `rows`: Número de filas de bloques
  - `cols`: Número de columnas de bloques

### Methods
- `method void draw()`
  - Dibuja todos los bloques activos

- `method void checkCollision(Ball ball)`
  - Verifica colisiones entre la pelota y todos los bloques
  - Destruye bloques al colisionar

- `method boolean allBlocksDestroyed()`
  - Retorna true si todos los bloques fueron destruidos

- `method int getRemainingBlocks()`
  - Retorna el número de bloques activos

- `method void dispose()`
  - Libera memoria de todos los bloques

---

## CollisionDetector

Clase con funciones estáticas para detección de colisiones.

### Functions
- `function boolean checkBallPaddle(Ball ball, Paddle paddle)`
  - Verifica colisión entre pelota y paleta
  - Retorna true si hay colisión

- `function boolean checkBallBlock(Ball ball, Block block)`
  - Verifica colisión entre pelota y bloque
  - Retorna true si hay colisión

- `function boolean checkBallWalls(Ball ball, int screenWidth, int screenHeight)`
  - Verifica colisión entre pelota y paredes
  - Retorna true si hay colisión

- `function boolean rectCollision(int x1, int y1, int w1, int h1, int x2, int y2, int w2, int h2)`
  - Verifica colisión entre dos rectángulos
  - Parámetros: posición y dimensiones de ambos rectángulos
  - Retorna true si los rectángulos se solapan

---

## GameUI

Clase con funciones estáticas para renderizar la interfaz.

### Functions
- `function void drawScore(int score)`
  - Muestra la puntuación actual en pantalla

- `function void drawLives(int lives)`
  - Muestra el número de vidas restantes

- `function void drawLevel(int level)`
  - Muestra el nivel actual

- `function void showStartScreen()`
  - Muestra la pantalla de inicio del juego

- `function void showGameOver(int finalScore)`
  - Muestra la pantalla de game over con puntuación final

- `function void showVictory(int finalScore)`
  - Muestra la pantalla de victoria con puntuación final

- `function void showPauseScreen()`
  - Muestra la pantalla de pausa

- `function void clearScreen()`
  - Limpia toda la pantalla

---

## Códigos de Tecla (Keyboard)

Constantes útiles para entrada del teclado:
- Flecha Izquierda: 130
- Flecha Derecha: 132
- Flecha Arriba: 131
- Flecha Abajo: 133
- Espacio: 32
- Q: 81
- ESC: 140

---

## Constantes del Sistema

### Dimensiones de Pantalla
- Screen Width: 512
- Screen Height: 256

### Colores
- Negro (background): false
- Blanco (foreground): true

---

## Notas de Implementación

1. **Gestión de Memoria**: Todos los objetos creados con `new` deben ser liberados con `dispose()`

2. **Coordenadas**: El origen (0,0) está en la esquina superior izquierda

3. **Velocidad**: Usar enteros para velocidad (sin flotantes en Jack)

4. **Colisiones**: Implementar con lógica de solapamiento de rectángulos (AABB)

5. **Renderizado**: Usar `Screen.setColor()` antes de dibujar para establecer color
