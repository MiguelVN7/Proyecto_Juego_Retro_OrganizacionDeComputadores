# 🚀 Guía Rápida de Compilación y Prueba

## Prerequisitos

- Nand2Tetris Software Suite instalado
- JackCompiler disponible en el PATH o en el directorio de herramientas

---

## 📦 Compilación

### Opción 1: Usar el script de compilación (Linux/Mac)

```bash
cd src/
# Buscar JackCompiler en tu instalación de Nand2Tetris
/path/to/nand2tetris/tools/JackCompiler.sh .
```

### Opción 2: Compilar manualmente

```bash
cd src/
# Compilar todos los archivos .jack
java -classpath /path/to/nand2tetris/tools/bin/classes Hack.Compiler.JackCompiler .
```

### Verificar compilación exitosa

Deberías ver que se actualizan (o crean) los siguientes archivos `.vm`:

```
✅ Ball.vm
✅ Block.vm
✅ BlockGrid.vm
✅ BreakoutGame.vm         ← MODIFICADO (loop optimizado)
✅ CollisionDetector.vm
✅ GameUI.vm
✅ Main.vm
✅ Paddle.vm               ← MODIFICADO (añadido reset())
```

---

## 🎮 Ejecución en CPU Emulator

### Paso 1: Abrir CPU Emulator

```bash
/path/to/nand2tetris/tools/CPUEmulator.sh
```

O en Windows:
```cmd
C:\nand2tetris\tools\CPUEmulator.bat
```

### Paso 2: Cargar el directorio

1. Ir a `File` → `Load Program`
2. Navegar al directorio `src/`
3. Seleccionar **el directorio completo** (no un archivo individual)
4. El emulador cargará automáticamente todos los `.vm`

### Paso 3: Configurar velocidad inicial

⚠️ **IMPORTANTE**: Antes de ejecutar, configura el **speed slider** en **MEDIO**

```
Lento  ←━━━━━●━━━━━→  Rápido
         ↑
      MEDIO (recomendado para primera prueba)
```

### Paso 4: Ejecutar

1. Click en `Run` (o presiona F5)
2. Deberías ver la **pantalla de inicio** del juego en pocos segundos
3. Presiona **ESPACIO** para iniciar el juego

---

## 🧪 Plan de Pruebas

### ✅ Test 1: Velocidad Media (2-3 minutos)

1. **Speed slider**: MEDIO
2. **Acción**: Presionar Space, jugar normalmente
3. **Resultado esperado**:
   - ✅ Bola se mueve a velocidad constante y jugable
   - ✅ No hay parpadeo excesivo
   - ✅ Paddle responde suavemente a las flechas

### ✅ Test 2: Velocidad Rápida (2-3 minutos)

1. **Speed slider**: RÁPIDO (máximo)
2. **Acción**: Presionar Space, jugar normalmente
3. **Resultado esperado**:
   - ✅ Velocidad similar a MEDIO (no turbo mode)
   - ✅ Juego completamente jugable
   - ✅ Sin bloqueos ni freezes

### ✅ Test 3: Transición de Pérdida de Vida (30 segundos)

1. **Acción**: Dejar caer la bola intencionalmente
2. **Resultado esperado**:
   - ✅ Pausa breve (~400ms)
   - ✅ Bola y paddle se reposicionan
   - ✅ Juego continúa sin congelarse
   - ✅ Contador de vidas decrece

### ✅ Test 4: Modo DEBUG (1 minuto)

1. **Preparación**: 
   - Editar `src/BreakoutGame.jack`, línea 49
   - Cambiar `let DEBUG = false;` → `let DEBUG = true;`
   - Recompilar
2. **Acción**: Ejecutar y empezar a jugar
3. **Resultado esperado**:
   - ✅ Esquina superior derecha muestra:
     ```
     F:120
     T:40
     ```
   - ✅ F (frame) aumenta de 1 en 1
   - ✅ T (tick) aumenta cada 3 frames (si UPDATE_EVERY=3)

### ✅ Test 5: Cambio de Velocidad en Caliente (2 minutos)

1. **Acción**: Mientras el juego está corriendo, mover el speed slider
2. **Resultado esperado**:
   - ✅ El juego mantiene velocidad consistente
   - ✅ Puede haber ligera variación, pero NO modo turbo
   - ✅ No se congela al cambiar el slider

### ✅ Test 6: Game Over y Reinicio (1 minuto)

1. **Acción**: Perder todas las vidas (3)
2. **Resultado esperado**:
   - ✅ Pantalla de Game Over sin freeze
   - ✅ Presionar Q → sale del juego
   - ✅ Presionar Enter → vuelve al menú

### ✅ Test 7: Victoria (opcional, requiere destruir todos los bloques)

1. **Acción**: Destruir todos los bloques
2. **Resultado esperado**:
   - ✅ Pantalla de Victoria sin freeze
   - ✅ Score final visible
   - ✅ Q para salir, Enter para menú

---

## ⚙️ Ajuste de Parámetros (Tuning)

Si necesitas ajustar la velocidad, edita `src/BreakoutGame.jack`, líneas 47-52:

```jack
let UPDATE_EVERY = 3;       // ← Cambiar este valor
let FRAME_WAIT_MS = 2;      // ← O este valor
let DEBUG = false;          // ← true para debug
```

### Tabla de Ajuste Rápido

| Problema                  | Solución                              |
|---------------------------|---------------------------------------|
| Bola muy lenta            | `UPDATE_EVERY = 2`                    |
| Bola muy rápida           | `UPDATE_EVERY = 4` o `5`              |
| Juego lagueado            | `FRAME_WAIT_MS = 1`                   |
| CPU al 100% en emulador   | `FRAME_WAIT_MS = 3` o `4`             |
| Quiero ver debug info     | `DEBUG = true`                        |

Después de cambiar los valores, **recompilar** y **recargar** en CPU Emulator.

---

## 🐛 Troubleshooting

### Problema: "Compilation error"

**Causa**: Sintaxis inválida en Jack  
**Solución**:
1. Revisar el output del compilador
2. Verificar que todos los archivos `.jack` estén presentes
3. Verificar que no haya caracteres especiales

### Problema: "Cannot load VM files"

**Causa**: Directorio incorrecto o archivos `.vm` faltantes  
**Solución**:
1. Asegurarse de cargar el directorio `src/`, no un archivo individual
2. Verificar que todos los `.vm` existan
3. Recompilar si es necesario

### Problema: Pantalla negra en el emulador

**Causa**: El programa no está ejecutándose  
**Solución**:
1. Presionar `Run` (F5)
2. Verificar que el slider de animación esté en una posición razonable
3. Revisar que no haya errores de compilación

### Problema: El juego va demasiado rápido/lento

**Causa**: Parámetros no ajustados para tu sistema  
**Solución**: Ver tabla de ajuste arriba

### Problema: El juego se congela al perder una vida

**Causa**: Versión antigua del código (antes de la optimización)  
**Solución**:
1. Verificar que `BreakoutGame.jack` tiene el método `loseLifeTransition()`
2. Recompilar completamente
3. Verificar que la línea con `Sys.wait(400)` esté presente

---

## 📊 Métricas de Performance Esperadas

Con `UPDATE_EVERY = 3` y `FRAME_WAIT_MS = 2`:

| Métrica               | Valor Esperado          |
|-----------------------|-------------------------|
| FPS efectivos         | ~60 FPS (física)        |
| Frame time            | ~2ms + overhead         |
| Physics update rate   | ~20 Hz (cada 3 frames)  |
| CPU usage (emulador)  | Bajo/Medio              |
| Responsiveness        | Suave y jugable         |

---

## 📝 Checklist Pre-Entrega

Antes de presentar al profesor:

- [ ] Compilar sin errores
- [ ] Ejecutar Test 1 (velocidad media) → ✅
- [ ] Ejecutar Test 2 (velocidad rápida) → ✅
- [ ] Ejecutar Test 3 (pérdida de vida) → ✅
- [ ] Verificar que no hay freezes ni bloqueos
- [ ] Verificar que `DEBUG = false` (modo producción)
- [ ] Limpiar archivos temporales si los hay
- [ ] Preparar explicación de parámetros tunables
- [ ] Tener diagrama de flujo a mano (docs/DIAGRAMA_FLUJO.txt)

---

## 🎓 Explicación para el Profesor

### Puntos Clave a Mencionar:

1. **Frame Limiter Real**: 
   - Usamos `Sys.wait(FRAME_WAIT_MS)` en lugar de busy-loop
   - Esto desacopla la velocidad del juego del CPU slider

2. **Física Normalizada**:
   - La bola se actualiza solo cada `UPDATE_EVERY` frames
   - Esto garantiza velocidad constante independiente del emulador

3. **Dirty Rectangle Rendering**:
   - No llamamos `Screen.clearScreen()` en cada frame
   - Solo borramos y redibujamos lo que cambió (bola y paddle)
   - Esto elimina parpadeo y mejora performance

4. **Máquina de Estados**:
   - Transiciones claras entre estados (MENU, PLAYING, etc.)
   - Waits apropiados para evitar bucles apretados

5. **Tunability**:
   - Parámetros ajustables al inicio de la clase
   - Fácil adaptar a diferentes configuraciones del emulador

### Demostración en Vivo:

1. Mostrar juego corriendo en velocidad MEDIA → jugabilidad normal
2. Cambiar slider a RÁPIDO → sigue siendo jugable
3. Activar DEBUG mode → mostrar contadores estables
4. Cambiar `UPDATE_EVERY` en vivo → recompilar → ver diferencia

---

## 📚 Archivos de Referencia

- **Código optimizado**: `src/BreakoutGame.jack`, `src/Paddle.jack`
- **Documentación completa**: `docs/OPTIMIZACION_TIMING.md`
- **Diagrama de flujo**: `docs/DIAGRAMA_FLUJO.txt`
- **Resumen ejecutivo**: `docs/RESUMEN_CAMBIOS.md`
- **Tareas completadas**: `docs/TODO.md`

---

**¡Listo para entregar!** 🎉

Si tienes algún problema, revisa primero el troubleshooting y los parámetros tunables.
