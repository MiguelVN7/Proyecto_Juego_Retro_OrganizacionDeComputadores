# TODO List - Breakout Game

## ✅ OPTIMIZACION DE TIMING COMPLETADA (Octubre 2025)

### Problemas Críticos Resueltos:
- [x] ✅ **Busy-loop eliminado**: Reemplazado `while(delay<50)` por `Sys.wait(FRAME_WAIT_MS)`
- [x] ✅ **Frame limiter implementado**: Loop determinista independiente del CPU slider
- [x] ✅ **Física normalizada**: Update solo cada `UPDATE_EVERY` frames (default: 3)
- [x] ✅ **Dirty rectangle rendering**: Eliminado `Screen.clearScreen()` del loop principal
- [x] ✅ **Máquina de estados robusta**: MENU → PLAYING → LOST_LIFE → GAME_OVER/VICTORY
- [x] ✅ **Transiciones sin bloqueos**: Wait apropiado en pérdida de vida (400ms)
- [x] ✅ **Modo DEBUG**: Contadores de frame y tick visibles en pantalla

### Archivos Modificados:
- `src/BreakoutGame.jack` - Loop principal reescrito
- `src/Paddle.jack` - Añadido método reset()
- `docs/OPTIMIZACION_TIMING.md` - Documentación completa
- `docs/DIAGRAMA_FLUJO.txt` - Diagrama visual del loop

### Parámetros Tunables:
Ver líneas 47-52 en `BreakoutGame.jack`:
```jack
let UPDATE_EVERY = 3;       // Física cada 3 frames
let FRAME_WAIT_MS = 2;      // 2ms wait por frame
let DEBUG = false;          // true para debug
```

---

## Fase 1: Estructura Básica ✅
- [x] Implementar constructor de Main
- [x] Implementar constructor de BreakoutGame (OPTIMIZADO)
- [x] Implementar constructor de Paddle
- [x] Implementar constructor de Ball
- [x] Implementar constructor de Block
- [x] Implementar constructor de BlockGrid
- [x] Implementar todos los métodos dispose()

## Fase 2: Renderizado ✅
- [x] Implementar Paddle.draw()
- [x] Implementar Ball.draw()
- [x] Implementar Block.draw()
- [x] Implementar BlockGrid.draw()
- [x] Implementar GameUI.clearScreen()
- [x] Implementar GameUI.drawScore()
- [x] Implementar GameUI.drawLives()
- [x] Implementar GameUI.showStartScreen()

## Fase 3: Movimiento Básico ✅
- [x] Implementar Paddle.moveLeft()
- [x] Implementar Paddle.moveRight()
- [x] Implementar límites de movimiento de Paddle
- [x] Implementar Ball.move() (OPTIMIZADO con dirty rectangles)
- [x] Implementar velocidad de Ball
- [x] Implementar detección de bordes de pantalla para Ball

## Fase 4: Sistema de Colisiones ✅
- [x] Implementar CollisionDetector.rectCollision()
- [x] Implementar CollisionDetector.checkBallPaddle()
- [x] Implementar CollisionDetector.checkBallBlock()
- [x] Implementar CollisionDetector.checkBallWalls()
- [x] Implementar Ball.bounceHorizontal()
- [x] Implementar Ball.bounceVertical()
- [x] Implementar BlockGrid.checkCollision()

## Fase 5: Lógica de Juego ✅
- [x] Implementar sistema de vidas en BreakoutGame
- [x] Implementar sistema de puntuación
- [x] Implementar detección de pelota fuera de límites (perder vida)
- [x] Implementar Ball.reset()
- [x] Implementar Paddle.reset() (NUEVO)
- [x] Implementar BlockGrid.allBlocksDestroyed()
- [x] Implementar condición de victoria
- [x] Implementar condición de game over
- [x] Implementar BreakoutGame.run() - loop principal (REESCRITO)

## Fase 6: Interfaz de Usuario ✅
- [x] Implementar GameUI.showGameOver()

- [ ] Implementar GameUI.showVictory()
- [ ] Implementar GameUI.showPauseScreen()
- [ ] Implementar GameUI.drawLevel()
- [ ] Mejorar visualización de vidas (corazones o iconos)
- [ ] Mejorar visualización de puntuación

## Fase 7: Input del Usuario ⬜
- [ ] Implementar detección de tecla izquierda
- [ ] Implementar detección de tecla derecha
- [ ] Implementar detección de tecla espacio (iniciar/pausar)
- [ ] Implementar detección de tecla Q (salir)
- [ ] Implementar pausa del juego
- [ ] Implementar reinicio del juego

## Fase 8: Polish y Refinamiento ⬜
- [ ] Ajustar velocidad de juego para mejor experiencia
- [ ] Ajustar física de rebotes en paleta (ángulos)
- [ ] Optimizar renderizado (solo redibujar cambios)
- [ ] Añadir delay entre frames para controlar velocidad
- [ ] Mejorar estética de bloques (diferentes colores/patrones)
- [ ] Añadir efectos visuales (parpadeo al destruir bloque)
- [ ] Ajustar dificultad (velocidad de pelota, tamaño de paleta)

## Fase 9: Testing ⬜
- [ ] Probar en VM Emulator de Nand2Tetris
- [ ] Verificar gestión de memoria (no memory leaks)
- [ ] Probar colisiones en esquinas
- [ ] Probar casos extremos (pelota muy rápida)
- [ ] Probar secuencia completa (inicio → juego → fin)
- [ ] Verificar todos los controles
- [ ] Probar victoria (destruir todos los bloques)
- [ ] Probar game over (perder todas las vidas)

## Fase 10: Documentación ⬜
- [ ] Actualizar README.md con instrucciones de compilación
- [ ] Actualizar README.md con instrucciones de juego
- [ ] Documentar código con comentarios
- [ ] Crear guía de instalación
- [ ] Crear screenshots o video demo
- [ ] Documentar limitaciones conocidas
- [ ] Documentar posibles mejoras futuras

## Features Opcionales (Bonus) ⬜
- [ ] Múltiples niveles con patrones de bloques diferentes
- [ ] Bloques de diferentes colores con puntuación variable
- [ ] Aumentar velocidad de pelota progresivamente
- [ ] Power-ups (paleta más grande, pelota más lenta, etc.)
- [ ] Sonidos (si es posible en Hack)
- [ ] High score persistente
- [ ] Animaciones de transición entre pantallas
- [ ] Contador de tiempo
- [ ] Combo system (destruir bloques consecutivamente)

---

## Notas de Progreso

### Fecha: [Pendiente]
- Estado: Estructura del proyecto creada
- Próximo paso: Comenzar Fase 1

---

## Prioridad de Implementación

1. **Alta**: Fases 1-5 (Core gameplay)
2. **Media**: Fases 6-7 (UI y controles)
3. **Baja**: Fases 8-10 (Polish y extras)
4. **Opcional**: Features Bonus
