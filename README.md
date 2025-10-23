# Breakout - Juego Retro en Jack

Implementación del clásico juego arcade **Breakout** desarrollado en lenguaje Jack para la plataforma Nand2Tetris.

## ⚡ OPTIMIZACIÓN v1.0 - Loop Determinista Implementado

**IMPORTANTE**: Este proyecto ha sido optimizado con un **loop de juego determinista** que funciona independientemente del speed slider del CPU Emulator. Ver [docs/RESUMEN_FINAL.md](docs/RESUMEN_FINAL.md) para detalles completos.

### 🎯 Mejoras Clave:
- ✅ **Frame limiter real** con `Sys.wait()` - no más busy-loops
- ✅ **Física normalizada** - velocidad constante independiente del emulador
- ✅ **Dirty rectangle rendering** - sin parpadeo
- ✅ **Máquina de estados robusta** - sin bloqueos
- ✅ **Parámetros tunables** - fácil ajuste de velocidad

### ⚙️ Ajuste Rápido:
Editar `src/BreakoutGame.jack`, líneas 47-52:
```jack
let UPDATE_EVERY = 3;       // Física cada 3 frames
let FRAME_WAIT_MS = 2;      // 2ms wait por frame
let DEBUG = false;          // true para debug
```

---

## 📋 Descripción

Breakout es un juego arcade donde el jugador controla una paleta en la parte inferior de la pantalla para mantener una pelota en juego y destruir todos los bloques ubicados en la parte superior. Este proyecto es parte del curso de Organización de Computadores y demuestra la programación a bajo nivel usando el lenguaje Jack.

## 🎮 Características del Juego

- ✅ Paleta controlable con teclas de flecha
- ✅ Física de pelota con rebotes realistas **[OPTIMIZADA]**
- ✅ Sistema de bloques destructibles
- ✅ Sistema de vidas (3 vidas iniciales)
- ✅ Sistema de puntuación
- ✅ Detección de colisiones precisa
- ✅ Pantallas de inicio, victoria y game over
- ✅ Sistema de pausa
- ✅ **Loop determinista** - funciona igual en cualquier velocidad de emulador
- ✅ **Modo DEBUG** - visualiza contadores de frame y tick

## 🕹️ Controles

| Tecla | Acción |
|-------|--------|
| **←** (Flecha Izquierda) | Mover paleta a la izquierda |
| **→** (Flecha Derecha) | Mover paleta a la derecha |
| **Espacio** | Iniciar juego / Pausar |
| **Q** | Salir del juego |
| **Enter** | Reiniciar (desde Game Over/Victory) |

## 📁 Estructura del Proyecto

```
Proyecto_Juego_Retro_OrganizacionDeComputadores/
├── src/                      # Código fuente en Jack
│   ├── Main.jack            # Punto de entrada del programa
│   ├── BreakoutGame.jack    # Controlador principal del juego
│   ├── Paddle.jack          # Clase de la paleta
│   ├── Ball.jack            # Clase de la pelota
│   ├── Block.jack           # Clase de bloque individual
│   ├── BlockGrid.jack       # Gestor de todos los bloques
│   ├── CollisionDetector.jack # Utilidad para detección de colisiones
│   └── GameUI.jack          # Interfaz de usuario
├── docs/                     # Documentación
│   ├── design.md            # Documento de diseño del juego
│   ├── api.md               # Documentación de la API
│   └── TODO.md              # Lista de tareas
├── assets/                   # Recursos adicionales
└── README.md                # Este archivo
```

## 🔧 Requisitos

- **Nand2Tetris Software Suite** (incluye VM Emulator y Jack Compiler)
- Descargar desde: [nand2tetris.org](https://www.nand2tetris.org/)

## 🚀 Compilación y Ejecución

### Paso 1: Compilar el código Jack

```bash
# Navegar al directorio src
cd src

# Compilar con el Jack Compiler
JackCompiler .
```

Esto generará archivos `.vm` para cada archivo `.jack`.

### Paso 2: Ejecutar en el VM Emulator

1. Abrir el **VM Emulator** de Nand2Tetris
2. Cargar la carpeta `src` que contiene los archivos `.vm`
3. Configurar la velocidad de ejecución (recomendado: Fast o Faster)
4. Hacer clic en **Run** para iniciar el juego

## 📚 Arquitectura del Juego

### Clases Principales

#### `Main`
Punto de entrada del programa que inicializa y ejecuta el juego.

#### `BreakoutGame`
Controlador principal que maneja:
- Loop de juego
- Estado del juego
- Sistema de vidas y puntuación
- Coordinación entre componentes

#### `Paddle`
Representa la paleta controlada por el jugador:
- Movimiento hor izontal
- Límites de pantalla
- Renderizado

#### `Ball`
Representa la pelota del juego:
- Movimiento con velocidad constante
- Física de rebotes
- Detección de límites

#### `Block` y `BlockGrid`
Sistema de bloques destructibles:
- `Block`: Bloque individual con estado
- `BlockGrid`: Gestiona matriz de bloques y colisiones

#### `CollisionDetector`
Utilidad con funciones estáticas para:
- Detección de colisión pelota-paleta
- Detección de colisión pelota-bloque
- Detección de colisión con paredes

#### `GameUI`
Maneja toda la interfaz visual:
- Pantallas de inicio/fin
- HUD con puntuación y vidas
- Mensajes del juego

## 🎯 Objetivos de Aprendizaje

Este proyecto demuestra:

1. **Programación Orientada a Objetos en Jack**
   - Clases y constructores
   - Métodos y funciones
   - Gestión de memoria manual

2. **Estructuras de Datos**
   - Arrays para gestión de bloques
   - Estados del juego

3. **Algoritmos**
   - Detección de colisiones (AABB)
   - Física simple de rebotes
   - Loop de juego

4. **Programación de Sistemas**
   - Manejo de entrada del teclado
   - Renderizado en pantalla
   - Control de flujo del programa

## 📊 Parámetros del Juego

| Parámetro | Valor |
|-----------|-------|
| Pantalla | 512 x 256 píxeles |
| Paleta | 60 x 8 píxeles |
| Pelota | Radio de 4 píxeles |
| Bloques | 45 x 10 píxeles |
| Filas de bloques | 5 |
| Columnas de bloques | 10 |
| Vidas iniciales | 3 |
| Puntos por bloque | 10 |

## 🐛 Debugging

Para depurar el código:

1. Usar el VM Emulator con velocidad lenta
2. Verificar gestión de memoria (no memory leaks)
3. Revisar valores de variables en tiempo de ejecución
4. Probar casos extremos (colisiones en esquinas)

## 📝 Notas de Desarrollo

- Jack no soporta números flotantes, toda la física usa enteros
- Es importante llamar `dispose()` en todos los objetos para evitar memory leaks
- Las coordenadas tienen origen (0,0) en la esquina superior izquierda
- El renderizado debe optimizarse redibujando solo lo necesario

## 🔮 Mejoras Futuras

- [ ] Múltiples niveles con patrones diferentes
- [ ] Bloques de diferentes colores y puntuaciones
- [ ] Power-ups (paleta más grande, pelota más lenta)
- [ ] Velocidad de pelota progresiva
- [ ] Sistema de high score
- [ ] Efectos visuales mejorados

## 👥 Autor

**Miguel VN**
- Curso: Organización de Computadores
- Semestre: Sexto
- Universidad: Ingeniería de Sistemas

## 📜 Licencia

Este proyecto es parte de un trabajo académico para el curso de Organización de Computadores.

## 🙏 Agradecimientos

- Nand2Tetris por la plataforma educativa
- Inspiración en el Breakout original de Atari (1976)

---

**Estado del Proyecto:** 🚧 En Desarrollo

Para más información, consulta la documentación en la carpeta `docs/`.
