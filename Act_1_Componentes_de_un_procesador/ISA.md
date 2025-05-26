# INSTRUCTION SET ARCHITECTURE

## 1. ¿Qué significa que ARM sea una arquitectura RISC?

- **RISC** (Reduced Instruction Set Computer) significa que ARM utiliza un conjunto de instrucciones simplificado y optimizado.
- Características clave:
  - Instrucciones de tamaño fijo (generalmente 32 bits).
  - Operaciones de carga/almacenamiento (load/store) separadas de las operaciones aritméticas.
  - Mayor número de registros para reducir accesos a memoria.
  - Pipeline más eficiente gracias a la simplicidad de las instrucciones.

## 2. ¿Por qué la arquitectura ARM es popular en dispositivos móviles?
- **Bajo consumo de energía**: Diseño eficiente que prioriza el rendimiento por vatio.
- **Escalabilidad**: Licenciamiento flexible permite personalizaciones para diferentes necesidades.
- **Rendimiento equilibrado**: Adecuado para tareas multimedia y multitarea en smartphones/tablets.
- **Ecosistema**: Soporte masivo de fabricantes (Qualcomm, Apple, Samsung) y sistemas operativos (Android, iOS).

## 3. ¿En qué consiste la “Arquitectura Harvard modificada” en ARM?
- **Separación de buses** para instrucciones y datos (como en Harvard pura), pero con un **espacio de memoria unificado**.
- Ventajas:
  - Permite fetch de instrucciones y acceso a datos en paralelo.
  - Mantiene compatibilidad con memoria compartida para instrucciones y datos.

## 4. ¿Cuáles son las principales familias de procesadores ARM?
- **Cortex-A**: Para aplicaciones (smartphones, tablets, sistemas operativos complejos).
- **Cortex-R**: Tiempo real (automoción, industriales).
- **Cortex-M**: Microcontroladores (IoT, dispositivos embebidos de bajo consumo).
- **SecurCore**: Seguridad (tarjetas SIM, pagos).
- **Neoverse**: Infraestructura y servidores.

## 5. ¿Qué ventajas ofrece el set de instrucciones Thumb-2?
- **Mejor balance entre rendimiento y densidad de código**:
  - Combina instrucciones de 16 bits (Thumb) y 32 bits (ARM) en un solo ISA.
  - Reduce el tamaño del código (~30% menor que ARM puro) sin penalizar rendimiento.
  - No necesita cambio de modo entre Thumb y ARM.

## 6. ¿Por qué es relevante la comunidad ARM?
- **Estandarización**: Arquitectura dominante en móviles/embebidos.
- **Colaboración**: Empresas como NVIDIA, Qualcomm, y Apple contribuyen al ecosistema.
- **Herramientas**: Amplio soporte de compiladores (GCC, LLVM), RTOS, y librerías.
- **Open Source**: Proyectos como Mbed OS facilitan el desarrollo.

## 7. ¿Qué características distinguen al ARM Cortex-M4?
- **DSP integrado**: Instrucciones SIMD para procesamiento digital de señales.
- **FPU opcional**: Unidad de punto flotante para cálculos complejos.
- **Bajo consumo**: Modos sleep avanzados (ideal para IoT).
- **Núcleo eficiente**: Pipeline 3-etapas (Fetch, Decode, Execute).

## 8. ¿Qué tipos de registros básicos se encuentran en la arquitectura ARM Cortex-M?
- **Registros de propósito general (R0-R12)**: Para operaciones aritméticas y lógicas.
- **Registros especiales**:
  - **SP (R13)**: Stack Pointer (MSP/PSP para modos Thread/Handler).
  - **LR (R14)**: Link Register (dirección de retorno).
  - **PC (R15)**: Program Counter.
  - **APSR/xPSR**: Registros de estado (flags como Z, N, C, V).

## 9. ¿Para qué se utilizan los modos Thread y Interrupt en ARM Cortex-M?
- **Thread Mode**: Ejecución normal de código de aplicación.
- **Interrupt Mode (Handler Mode)**: Para manejo de excepciones/interrupciones (NVIC).
- Diferencias:
  - **Privilegios**: Thread puede ejecutarse sin privilegios (seguridad).
  - **Stack Pointer**: Thread usa PSP (opcional), Interrupt usa MSP.

## 10. ¿En qué consiste el mapa de memoria de 4 GB en Cortex-M?
- **Espacio lineal de 32 bits** (0x0000_0000 a 0xFFFF_FFFF) dividido en regiones:
  - **Código (0x0000_0000 - 0x1FFF_FFFF)**: Para firmware (Flash).
  - **SRAM (0x2000_0000 - 0x3FFF_FFFF)**: Memoria dinámica.
  - **Periféricos (0x4000_0000 - 0x5FFF_FFFF)**: Registros de hardware.
  - **RAM externa (0x6000_0000 - ...)**: Opcional para expansión.
  - **Sistema (0xE000_0000 - ...)**: NVIC, debug, etc.
 
# EJERCICIO
El siguiente codigo se basa solo en mover datos

```assembly
.syntax unified
.global _start
.text

_start:
    MOV R0, #42         @ Carga el valor inmediato 42 en R0
    MOV R1, #2561       @ Carga 2561 en R1 (nota: este valor puede no ser válido como inmediato)
    MOV R1, #2560       @ Sobrescribe R1 con 2560
    MOV R1, R0          @ Copia el valor de R0 a R1
    MOV R2, LR          @ Copia el valor del Link Register (R14) a R2
    MOV R3, R0, LSL #1  @ Desplazamiento lógico izquierdo de R0 (R3 = R0*2)
    MOV R4, R1, LSR #2  @ Desplazamiento lógico derecho de R1 (R4 = R1/4)
    MOV R5, R2, ASR #3  @ Desplazamiento aritmético derecho (preserva signo)
    MOV R6, R3, ROR #4  @ Rotación derecha de 4 bits
    MOVS R7, #100       @ Mueve 100 a R7 y actualiza flags
    MOVW R8, #0x1234    @ Carga 16 bits bajos (0x1234)
    MOVT R8, #0x5678    @ Carga 16 bits altos (R8 = 0x56781234)
    B .                 @ Bucle infinito (punto)
.end
```


## ANALISIS DEL CODIGO

### Diferencia entre desplazamiento lógico y aritmético
- **LSL/LSR (Logical Shift)**: 
  - Rellenan con **ceros** los bits vacíos.
  - LSL mueve bits hacia la izquierda (equivale a multiplicar por 2ⁿ).
  - LSR mueve bits hacia la derecha (equivale a división unsigned por 2ⁿ).

Valor:      0b1001_0110 (-106 en complemento a 2)
LSR #1:    0b0100_1011  (75)  ← Pierde el signo
ASR #1:    0b1100_1011  (-53) ← Mantiene el signo

- **ASR (Arithmetic Shift Right)**:
  - Preserva el **bit de signo** (MSB) en desplazamientos a la derecha.
  - Útil para divisiones de números **con signo** (ej: `-8 >> 1 = -4`).

### Aplicaciones para ASR vs LSR
- **ASR es crucial en**:
  - Procesamiento de señales con valores negativos (audio, sensores).
  - Operaciones matemáticas con enteros con signo.
  - Algoritmos de compresión (ej: JPEG donde los coeficientes DCT pueden ser negativos).

## Diferencia entre `MOV R0, #42` y `MOV R0, R1`
- `MOV R0, #42`: Carga el **valor inmediato 42** en R0.
- `MOV R0, R1`: Copia el **contenido de R1** a R0 (depende del valor actual de R1).

### Instrucción `MOVS` vs `MOV`
- `MOVS` actualiza los **flags** (N, Z) en el APSR según el resultado, mientras que `MOV` no.
- Ejemplo: `MOVS R7, #100` podría activar el flag **Z** si el resultado fuera cero.

### Uso combinado de `MOVW` y `MOVT`
- **MOVW**: Carga los 16 bits **bajos** de un valor (ej: `0x1234` en R8).
- **MOVT**: Carga los 16 bits **altos** en el mismo registro (ej: `0x5678` → R8 = `0x56781234`).
- **Razón**: ARM no puede cargar valores de 32 bits completos en una sola instrucción.

### Valores inmediatos y restricciones
- **Limitación**: Solo valores que pueden expresarse como **rotaciones de 8 bits** (ej: `0xFF` sí, `0x100` no directamente).
- **Máximo valor inmediato**: Depende del encoding, pero típicamente **12 bits útiles** (con rotaciones).

### Alternativa para números grandes
- Usar **carga en dos pasos** (`MOVW` + `MOVT`).
- Almacenar el valor en memoria y cargarlo con `LDR`.

### Hallazgos significativos (para discusión)
1. **Optimización de código**: Thumb-2 permite mezclar instrucciones de 16/32 bits para ahorrar espacio.
2. **Manejo de signo**: ASR vs LSR muestra cómo ARM maneja datos con/sin signo de hardware.
3. **Valores inmediatos**: La limitación afecta cómo se escriben constantes en ensamblador.
4. **Estructura de registro**: Uso de LR (R14) como registro especial para direcciones de retorno.
5. **Modo Thumb**: El código usa sintaxis unificada (`.syntax unified`), típica en Cortex-M.


# LLEVAR A ENSAMBLADOR 

# Soluciones de ejercicios de ensamblador

## Ejercicio 1: Condicional simple 

```assembly
CMP R0, #100      ; Compara R0 con 100
BGT ETIQUETA1     ; Si R0 > 100, salta a ETIQUETA1
B ETIQUETA2       ; Sino, salta a ETIQUETA2
```

## Ejercicio 2: Condicional doble 

```assembly
CMP R1, R2        ; Compara R1 con R2
BEQ IGUALES       ; Si son iguales, salta a IGUALES
BNE DIFERENTES    ; Si son diferentes, salta a DIFERENTES
```
## Ejercicio 3: Condicional encadenado 

```assembly
CMP R3, #10       ; Compara R3 con 10
BGE ETIQUETA_OK   ; Si R3 >= 10, salta a ETIQUETA_OK
BLT ETIQUETA_ERROR ; Si R3 < 10, salta a ETIQUETA_ERROR
```

## Ejercicio 4: Bucle While con Comparacion  

```assembly
BUCLE:
  CMP R0, #0      ; Compara R0 con 0
  BEQ FIN         ; Si R0 == 0, salta a FIN
  SUB R0, R0, #1  ; Decrementa R0 en 1
  B BUCLE         ; Repite el bucle
FIN:
```

## Ejercicio 5: Bucle while anidado (R1 < R2)
```assembly
BUCLE:
  CMP R1, R2      ; Compara R1 con R2
  BGE FIN         ; Si R1 >= R2, salta a FIN
  ADD R1, R1, #2  ; Incrementa R1 en 2
  CMP R1, R2      ; Compara R1 con R2
  BEQ SALIDA      ; Si son iguales, salta a SALIDA
  B BUCLE         ; Repite el bucle
FIN:
```

