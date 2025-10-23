# TODO List - Breakout Game

## Fase 1: Estructura Básica ⬜
- [ ] Implementar constructor de Main
- [ ] Implementar constructor de BreakoutGame
- [ ] Implementar constructor de Paddle
- [ ] Implementar constructor de Ball
- [ ] Implementar constructor de Block
- [ ] Implementar constructor de BlockGrid
- [ ] Implementar todos los métodos dispose()

## Fase 2: Renderizado ⬜
- [ ] Implementar Paddle.draw()
- [ ] Implementar Ball.draw()
- [ ] Implementar Block.draw()
- [ ] Implementar BlockGrid.draw()
- [ ] Implementar GameUI.clearScreen()
- [ ] Implementar GameUI.drawScore()
- [ ] Implementar GameUI.drawLives()
- [ ] Implementar GameUI.showStartScreen()

## Fase 3: Movimiento Básico ⬜
- [ ] Implementar Paddle.moveLeft()
- [ ] Implementar Paddle.moveRight()
- [ ] Implementar límites de movimiento de Paddle
- [ ] Implementar Ball.move()
- [ ] Implementar velocidad de Ball
- [ ] Implementar detección de bordes de pantalla para Ball

## Fase 4: Sistema de Colisiones ⬜
- [ ] Implementar CollisionDetector.rectCollision()
- [ ] Implementar CollisionDetector.checkBallPaddle()
- [ ] Implementar CollisionDetector.checkBallBlock()
- [ ] Implementar CollisionDetector.checkBallWalls()
- [ ] Implementar Ball.bounceHorizontal()
- [ ] Implementar Ball.bounceVertical()
- [ ] Implementar BlockGrid.checkCollision()

## Fase 5: Lógica de Juego ⬜
- [ ] Implementar sistema de vidas en BreakoutGame
- [ ] Implementar sistema de puntuación
- [ ] Implementar detección de pelota fuera de límites (perder vida)
- [ ] Implementar Ball.reset()
- [ ] Implementar BlockGrid.allBlocksDestroyed()
- [ ] Implementar condición de victoria
- [ ] Implementar condición de game over
- [ ] Implementar BreakoutGame.run() - loop principal

## Fase 6: Interfaz de Usuario ⬜
- [ ] Implementar GameUI.showGameOver()
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
