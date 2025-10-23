# Diseño del Juego Breakout

## Descripción General
Breakout es un juego arcade clásico donde el jugador controla una paleta en la parte inferior de la pantalla para mantener una pelota en juego y destruir bloques en la parte superior.

## Objetivo del Juego
Destruir todos los bloques golpeándolos con la pelota sin dejar que la pelota caiga por debajo de la paleta.

## Componentes Principales

### 1. Paleta (Paddle)
- Controlada por el jugador usando las teclas de flecha izquierda/derecha
- Se mueve horizontalmente en la parte inferior de la pantalla
- No puede salirse de los límites de la pantalla

### 2. Pelota (Ball)
- Se mueve constantemente en diagonal
- Rebota contra paredes, paleta y bloques
- Si cae por debajo de la paleta, el jugador pierde una vida

### 3. Bloques (Blocks)
- Organizados en filas en la parte superior de la pantalla
- Desaparecen cuando son golpeados por la pelota
- Cada bloque otorga puntos al ser destruido

### 4. Sistema de Juego
- El jugador comienza con 3 vidas
- Puntuación aumenta al destruir bloques
- El nivel se completa cuando todos los bloques son destruidos
- Game Over cuando se pierden todas las vidas

## Mecánicas de Juego

### Controles
- **Flecha Izquierda**: Mover paleta a la izquierda
- **Flecha Derecha**: Mover paleta a la derecha
- **Espacio**: Iniciar juego / Pausar
- **Q**: Salir del juego

### Física
- La pelota mantiene velocidad constante
- El ángulo de rebote depende del punto de impacto en la paleta
- Rebotes en paredes y bloques son reflejos simples

### Sistema de Puntuación
- Bloque destruido: 10 puntos
- Bonus por velocidad de completado
- Bonus por vidas restantes al finalizar nivel

## Estructura de Clases

### Main
- Punto de entrada del programa
- Inicializa y ejecuta el juego

### BreakoutGame
- Controlador principal del juego
- Maneja el loop de juego
- Controla estado, puntuación y vidas

### Paddle
- Representa la paleta del jugador
- Maneja movimiento y renderizado

### Ball
- Representa la pelota
- Maneja movimiento, velocidad y rebotes

### Block
- Representa un bloque individual
- Maneja estado y renderizado

### BlockGrid
- Gestiona todos los bloques del nivel
- Maneja colisiones con bloques

### CollisionDetector
- Utilidad para detección de colisiones
- Funciones estáticas reutilizables

### GameUI
- Maneja toda la interfaz visual
- Muestra puntuación, vidas y mensajes

## Pantallas del Juego

1. **Pantalla de Inicio**
   - Título del juego
   - Instrucciones básicas
   - "Presiona ESPACIO para comenzar"

2. **Pantalla de Juego**
   - Área de juego principal
   - HUD con puntuación y vidas
   - Bloques, pelota y paleta

3. **Pantalla de Pausa**
   - "PAUSA"
   - Instrucciones para continuar

4. **Pantalla de Game Over**
   - "GAME OVER"
   - Puntuación final
   - Opción para reiniciar

5. **Pantalla de Victoria**
   - "¡VICTORIA!"
   - Puntuación final
   - Mensaje de felicitación

## Parámetros de Configuración

### Dimensiones de Pantalla (Hack Computer)
- Ancho: 512 píxeles
- Alto: 256 píxeles

### Paleta
- Ancho: 60 píxeles
- Alto: 8 píxeles
- Velocidad: 5 píxeles por frame

### Pelota
- Radio: 4 píxeles
- Velocidad inicial: 3 píxeles por frame

### Bloques
- Ancho: 45 píxeles
- Alto: 10 píxeles
- Filas: 5
- Columnas: 10
- Espaciado: 2 píxeles

### Juego
- Vidas iniciales: 3
- FPS objetivo: 30-60 (depende de la implementación)

## Fases de Implementación

### Fase 1: Estructura Básica
- Crear todas las clases
- Implementar constructores y dispose
- Setup básico de Main

### Fase 2: Renderizado
- Implementar draw() en todas las clases
- Dibujar elementos básicos en pantalla
- Implementar GameUI básico

### Fase 3: Movimiento
- Implementar movimiento de paleta
- Implementar movimiento de pelota
- Detección de límites de pantalla

### Fase 4: Colisiones
- Implementar CollisionDetector
- Pelota rebota en paredes
- Pelota rebota en paleta
- Pelota destruye bloques

### Fase 5: Lógica de Juego
- Sistema de vidas
- Sistema de puntuación
- Condiciones de victoria/derrota
- Reinicio de nivel

### Fase 6: Polish
- Pantallas de inicio/fin
- Efectos visuales mejorados
- Ajuste de dificultad
- Testing y debugging

## Consideraciones Técnicas

### Limitaciones de Jack
- No hay números flotantes (usar enteros para todo)
- Gestión manual de memoria (dispose)
- Recursos limitados del Hack Computer

### Optimizaciones
- Redibujar solo lo necesario
- Usar operaciones bit a bit cuando sea posible
- Minimizar llamadas a funciones costosas

### Testing
- Probar en el VM Emulator de Nand2Tetris
- Verificar gestión de memoria
- Probar casos extremos (esquinas, múltiples colisiones)
