# Breakout - Juego Retro en Jack

Implementación del clásico juego arcade **Breakout** desarrollada en lenguaje Jack para la plataforma Nand2Tetris.

## Nota Importante

El juego se puede compilar usando el Software en línea de Nand2Tetris, específicamente el jack compiler, ya luego se puede correr ahí mismo dándole a la opción de run, con el VM EMulator.
Adicionalmente, dentro del emulador, para que el juego funcione bien es necesario deslizar la barra de velocidad de la simulación para ponerla en "fast" (del todo a la derecha).

## Optimización del Loop de Juego

Este proyecto incorpora un **loop de juego determinista** que se comporta de forma estable.

### Mejoras clave

- Loop único de juego con limitador de frames mediante `Sys.wait(FRAME_WAIT_MS)`
- Física de la pelota desacoplada del slider del emulador
- Renderizado incremental (no se hace `clearScreen` en cada frame de juego)
- Máquina de estados clara: MENÚ, JUGANDO, PÉRDIDA DE VIDA, GAME OVER, NIVEL COMPLETADO, VICTORIA
- Parámetros ajustables para velocidad de juego, paleta y pelota

### Ajuste rápido de velocidad global

En `src/BreakoutGame.jack`, dentro del constructor:

```jack
let FRAME_WAIT_MS = 15;   // Tiempo de espera por frame en milisegundos
let DEBUG = false;        // true para mostrar información de depuración
```

- Aumentar `FRAME_WAIT_MS` hace el juego más lento y suave.
- Disminuir `FRAME_WAIT_MS` hace el juego más rápido (evitar valores muy bajos para no generar loops demasiado apretados).

## Descripción general

Breakout es un juego arcade donde el jugador controla una paleta en la parte inferior de la pantalla para mantener una pelota en juego y destruir todos los bloques ubicados en la parte superior.  
Este proyecto es parte del curso de Organización de Computadores y demuestra la programación a bajo nivel usando el lenguaje Jack sobre la arquitectura Hack.

## Características del juego

- Paleta controlable con teclas de flecha izquierda/derecha
- Física de pelota con rebotes realistas y colisiones optimizadas
- Sistema de bloques destructibles organizado en una cuadrícula
- Sistema de vidas (3 vidas iniciales)
- Sistema de puntuación
- Dos niveles:
  - Nivel 1: menos filas de bloques (más fácil)
  - Nivel 2: todas las filas activas y pelota más rápida
- Pantallas de inicio, nivel completado, victoria y game over
- Sistema de pausa con menú de pausa superpuesto
- Loop determinista que se comporta igual en cualquier velocidad del emulador
- Modo de depuración opcional

## Controles

| Tecla | Acción |
|-------|--------|
| Flecha izquierda | Mover la paleta a la izquierda |
| Flecha derecha  | Mover la paleta a la derecha |
| Espacio (en menú) | Iniciar el juego (Nivel 1) |
| Espacio (en juego) | Pausar / reanudar |
| Espacio (pantalla de nivel completado) | Pasar al siguiente nivel |
| Q (en menú) | Salir del juego (cerrar ejecución) |
| Q (en pantallas de Game Over, Victoria, Nivel completado) | Volver al menú principal |
| Enter (en Game Over / Victoria) | Reiniciar partida desde Nivel 1 |

## Estructura del proyecto

```text
Proyecto_Juego_Retro_OrganizacionDeComputadores/
├── src/                      # Código fuente en Jack
│   ├── Main.jack             # Punto de entrada del programa
│   ├── BreakoutGame.jack     # Controlador principal del juego y loop de estados
│   ├── Paddle.jack           # Clase de la paleta
│   ├── Ball.jack             # Clase de la pelota
│   ├── Block.jack            # Clase de bloque individual
│   ├── BlockGrid.jack        # Gestor de la cuadrícula de bloques y niveles
│   ├── CollisionDetector.jack# Utilidad para detección de colisiones
│   └── GameUI.jack           # Interfaz de usuario (HUD y pantallas)
└── README.md                 # Este archivo
```

## Requisitos

- Nand2Tetris Software Suite (incluye VM Emulator y Jack Compiler)  
  Disponible en: `https://www.nand2tetris.org`

## Compilación y ejecución

### Paso 1: Compilar el código Jack

```bash
# Navegar al directorio src
cd src

# Compilar con el Jack Compiler
JackCompiler .
```

Esto generará archivos `.vm` para cada archivo `.jack`.

### Paso 2: Ejecutar en el VM Emulator

1. Abrir el VM Emulator de Nand2Tetris.
2. Cargar la carpeta `src` que contiene los archivos `.vm`.
3. Configurar la velocidad de ejecución (el juego es estable incluso en Fast).
4. Hacer clic en Run para iniciar el juego.

## Arquitectura del juego

### Clases principales

#### `Main`
Punto de entrada del programa. Crea una instancia de `BreakoutGame`, ejecuta `run()` y luego llama a `dispose()`.

#### `BreakoutGame`
Controlador principal que maneja:

- Loop de juego determinista
- Máquina de estados (menú, juego, pérdida de vida, game over, nivel completado, victoria)
- Sistema de vidas y puntuación
- Cambio de niveles y reinicios
- Coordinación entre `Ball`, `Paddle`, `BlockGrid` y `GameUI`

#### `Paddle`
Representa la paleta controlada por el jugador:

- Movimiento horizontal limitado por los bordes de la pantalla
- Renderizado mediante rectángulos llenos
- Velocidad configurada en el constructor:

```jack
// src/Paddle.jack
let speed = 5;  // píxeles por movimiento de la paleta
```

#### `Ball`
Representa la pelota del juego:

- Movimiento con velocidad constante en X e Y
- Física de rebotes contra paredes, paleta y bloques
- Métodos para cambiar y aumentar la velocidad:

```jack
// src/Ball.jack
let speed = 3;  // velocidad base (se usa en reset)
```

En el nivel 2 se invoca `ball.increaseSpeed()` para hacer el juego más desafiante.

#### `Block` y `BlockGrid`
Sistema de bloques destructibles:

- `Block`: bloque individual con posición, tamaño, estado (activo/inactivo) y puntos.
- `BlockGrid`: crea la matriz de bloques, dibuja todos los bloques, gestiona colisiones y niveles:
  - `reset(1)`: activa solo las primeras filas (nivel 1).
  - `reset(2)`: activa todas las filas (nivel 2).

#### `CollisionDetector`
Utilidad con funciones estáticas para:

- Detección de colisión pelota-paleta
- Detección de colisión pelota-bloque
- Cálculo de la dirección de impacto (horizontal o vertical) para rebotar correctamente

#### `GameUI`
Maneja toda la interfaz visual:

- Pantalla de inicio
- HUD (score, vidas, nivel) sin fugas de memoria (las etiquetas se dibujan una sola vez)
- Pantallas de pausa, nivel completado, victoria y game over
- Mensajes y elementos decorativos (bordes, barras de progreso opcional)

## Objetivos de aprendizaje

Este proyecto demuestra:

1. Programación orientada a objetos en Jack
   - Clases y constructores
   - Métodos y funciones
   - Gestión de memoria manual con `Memory.deAlloc`

2. Estructuras de datos
   - Uso de `Array` para gestionar colecciones de bloques
   - Manejo de estados del juego mediante enteros y banderas booleanas

3. Algoritmos
   - Detección de colisiones (AABB y variaciones para círculo-rectángulo)
   - Física simple de rebotes
   - Diseño de un loop de juego determinista

4. Programación de sistemas
   - Manejo de entrada desde `Keyboard`
   - Renderizado con la API `Screen` y `Output`
   - Control de flujo usando una máquina de estados

## Parámetros del juego

| Parámetro           | Valor                                  |
|---------------------|----------------------------------------|
| Resolución pantalla | 512 x 256 píxeles                     |
| Paleta              | 60 x 8 píxeles                        |
| Pelota              | Radio de 4 píxeles                    |
| Bloques             | 45 x 10 píxeles                       |
| Filas de bloques    | 5 (todas en nivel 2, menos en nivel 1)|
| Columnas de bloques | 10                                    |
| Vidas iniciales     | 3                                     |
| Puntos por bloque   | 10                                    |

## Depuración

Sugerencias para depurar el juego:

1. Ejecutar el VM Emulator en velocidad lenta al probar nueva lógica.
2. Activar `DEBUG = true` en `BreakoutGame` para ver el contador de frames.
3. Verificar gestión de memoria (uso correcto de `dispose` en objetos).
4. Probar colisiones en esquinas, paredes y bordes de la paleta y bloques.

## Notas de desarrollo

- Jack no soporta números de punto flotante; toda la física se implementa con enteros.
- Es importante llamar a `dispose()` en todos los objetos que usan memoria dinámica.
- El origen de coordenadas es (0,0) en la esquina superior izquierda de la pantalla.
- El renderizado se optimiza evitando llamar a `clearScreen` en cada frame y redibujando solo lo necesario.

## Estado del proyecto

Proyecto funcional con dos niveles jugables, loop determinista y lógica estable, adecuado como entrega para el curso de Organización de Computadores.


