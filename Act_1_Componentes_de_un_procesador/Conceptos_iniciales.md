# CONCEPTOS CLAVE 

## 1. CPU (Central Processing Unit)
### Definición Profunda
La **Unidad Central de Procesamiento** es un circuito digital superscalar que implementa el modelo de ejecución de instrucciones de una arquitectura específica mediante hardware semiconductor (generalmente CMOS en tecnologías FinFET modernas).

<img src="https://github.com/user-attachments/assets/e55e6fac-7794-461f-b05d-4b4aeee7b4dc" width="300px" height="150px" />

### PROCESADOR RISC

Un procesador RISC (Reduced Instruction Set Computer) es un tipo de arquitectura de procesador que se basa en un conjunto reducido y optimizado de instrucciones, diseñadas para ejecutarse rápidamente y de forma eficiente, generalmente en un solo ciclo de reloj.
# Comparación RISC vs CISC

| Característica          | RISC                              | CISC                              |
|-------------------------|-----------------------------------|-----------------------------------|
| Nº de instrucciones     | Bajo                              | Alto                              |
| Complejidad de instrucciones | Baja                         | Alta                              |
| Acceso a memoria        | Solo LOAD/STORE                  | Varias instrucciones acceden a memoria |
| Tamaño de instrucción   | Fijo (generalmente)              | Variable                          |
| Ejemplo                 | ARM, RISC-V                      | x86, x86-64                       |

<img src="https://github.com/user-attachments/assets/998b1d8c-6b21-44fa-ada9-a2fd49b4bb6c" width="200px" height="150px" />

### Arquitectura Detallada
#### Pipeline de Ejecución

- **Etapas en procesadores RISC**:
  
  1. **IF** (Instruction Fetch)
     - Lectura desde la memoria caché L1i (Instruction Cache)
     - Uso del Program Counter (PC) como puntero
     - Ancho de banda determinado por el bus de instrucciones (typically 64-256 bits en CPUs modernas)

  2. **ID** (Instruction Decode)
     - Decodificación mediante PLA (Programmable Logic Array) o microcódigo
     - Lectura del banco de registros (Register File)
     - Detección de riesgos estructurales y de datos

  3. **EX** (Execution)
     - Operaciones aritméticas en la ALU
     - Cálculo de direcciones para load/store
     - Ejecución en unidades especializadas (FPU, SIMD)

  4. **MEM** (Memory Access)
     - Acceso a caché L1d (Data Cache)
     - Manejo de miss/hit (typically 3-5 ciclos de penalización)
     - Escritura en buffer de almacenamiento

  5. **WB** (Write Back)
     - Escritura de resultados en el register file
     - Forwarding de resultados a etapas anteriores

## 2. ALU (Arithmetic Logic Unit)
### Diseño a Nivel de Transistores
- **Sumador Ripple-Carry**:
  - Diseño básico con propagación de carry
  - Latencia de O(n) para n bits
  - Implementación con compuertas XOR (Sum) y AND (Carry)

- **Sumador Carry-Lookahead**:
  - Bloques de 4 bits con generación/propagación
  - Ecuaciones lógicas:
    ```
    G = A AND B
    P = A XOR B
    C_{i+1} = G OR (P AND C_i)
    ```

- **Unidad Lógica**:
  - Operaciones soportadas:
    - AND, OR, XOR, NOT
    - Shift lógico/aritmético
    - Operaciones de máscara (bit manipulation)

- **Circuitos Especializados**:
  - Multiplicador Booth (radix-4 o radix-8)
  - Divisor SRT (Sweeney, Robertson, Tocher)
  - Unidad de conteo de población (POPCNT)

## 3. Registros
### Registros de Propósito General
Usados para cálculos temporales, almacenamiento de operandos
- **Características**:
  - Tamaño igual al ancho de palabra (32/64 bits)
  - Número típico: 16-32 registros enteros
  - Implementación como SRAM multi-ported (3-8 ports)

### Registros Específicos
#### Program Counter (PC)
Tienen funciones definidas por la arquitectura del procesador.

- Contador de 32/64 bits con lógica de incremento
- Múltiples fuentes de actualización:
  - Secuencial (+4 bytes típicamente)
  - Saltos relativos (offset codificado)
  - Saltos absolutos (registros o memoria)

#### Stack Pointer (SP)
- Puntero a memoria con auto-incremento/decremento
- Modos de direccionamiento:
  - Pre-decremento (push)
  - Post-incremento (pop)

#### Registro de Estado (FLAGS)
- Bits clave:
  - Z (Zero Flag): Resultado cero
  - C (Carry Flag): Acarreo en operaciones
  - N (Negative): Resultado negativo
  - V (Overflow): Desbordamiento aritmético
  - P (Parity): Paridad del resultado

## 4. Unidad de Control
La Unidad de Control coordina y dirige la ejecución de instrucciones en la CPU. Sus responsabilidades incluyen:
- Decodificar la instrucción obtenida de memoria.
- Generar señales de control para los demás bloques de la CPU.
- Sincronizar las operaciones mediante un reloj.

Puede estar implementada como:
- Unidad cableada (combinacional, más rápida).
- Unidad microprogramada (más flexible y compleja).
  

## 5. Buses
### Bus de Datos
- Transporta datos entre CPU, memoria y dispositivos periféricos.
- Es bidireccional.
- Su ancho (8, 16, 32, 64 bits) determina cuántos bits se pueden transferir a la vez.

- Características:
  - Ancho: 64-256 bits
  - Velocidad: 2-5 GT/s (GigaTransfers/sec)
  - Esquemas de clock: DDR (Double Data Rate)

### Bus de Direcciones
- Indica la ubicación en memoria donde se leerán o escribirán datos.
- Es unidireccional (CPU → memoria).
- u ancho define el espacio direccionable (ej.: 32 bits = 4 GB de memoria direccionable).
- 
- Características:
  - Ancho determina espacio direccionable (32/64 bits)
  - Protocolos de arbitraje (round-robin, priority-based)
  - Traducción de direcciones (MMU)

<img src="https://github.com/user-attachments/assets/aa47c2d7-2b2d-4231-8497-a34227a83455" width="200px" height="150px" />

## 6. Memorias
### RAM (Random Access Memory)

- Es volátil: pierde su contenido al apagar el sistema.
- Sirve como memoria principal del sistema.
- Almacena instrucciones y datos de programas en ejecución.
- De acceso aleatorio y lectura/escritura.

### ROM (Read Only Memory)

- Es no volátil: conserva su contenido sin energía.
- Almacena firmware y datos permanentes.
- Tradicionalmente de solo lectura, aunque variantes como EEPROM permiten escritura limitada.

#### ¿Son vigentes los terminos?
Sí. Aunque las tecnologías evolucionaron (RAM DDR5, Flash, etc.), los conceptos de RAM y ROM siguen siendo fundamentales y de uso habitual en informática y sistemas embebidos.

<img src="https://github.com/user-attachments/assets/368c0060-9762-4450-bf4b-e57cb4a5df60" width="200px" height="150px" />


## 7. Opcode
Un opcode (código de operación) es la parte de una instrucción de máquina que indica a la CPU qué operación debe realizar. Especifica el tipo de operación como:

- ADD: sumar dos operandos.
- MOV: mover datos de un lugar a otro.
- JMP: saltar a otra instrucción.

# PROGRAMA Y SU ALMACENAMIENTO 

## 1. ¿Qué es un programa y dónde se almacena?

**Definición de programa**:  
Un programa es un conjunto estructurado de instrucciones en código máquina (binario) que sigue la arquitectura del procesador objetivo, derivado de la compilación/ensamblado de código fuente.

**Ubicación de almacenamiento**:
- **En disco** (persistente):
  - Archivos binarios (`.exe`, `.elf`, `.bin`)
  - Sectores específicos del sistema de archivos
  - Formato estructurado (encabezados ELF/PE, secciones .text)

- **En memoria durante ejecución** (volátil):
  - Segmento de **código/texto** (memoria ROM virtual)
  - Caché L1i (Instruction Cache) del CPU
  - Mapeado mediante tablas de páginas (MMU)

## 2. Almacenamiento de comentarios

**Ejemplo de comentario**:  
`//variable tipo contador`

**Ubicaciones según fase**:

1. **En desarrollo**:
   - Archivo fuente original (ej. `app.c`, `main.py`)
   - Sistemas de control de versión (Git, SVN)
   - Metadata en IDEs (Visual Studio Code, Eclipse)

2. **Durante compilación**:
   - Eliminados en fase de preprocesamiento (C/C++)
   - No se incluyen en el .obj/.o intermedio
   - Excepciones:
     - Lenguajes interpretados (Python, JS): permanecen en el bytecode
     - Comentarios de documentación (Doxygen, Javadoc): generan metadata aparte

3. **En el binario final**:
   - Generalmente **no existen** en el ejecutable
   - Casos especiales:
     - Strings de depuración (sección `.debug_info`)
     - Firmware embebido (comentarios en scripts de linker)

## 3. Almacenamiento de variables

Dependiendo del tipo y contexto, una variable puede almacenarse en:

- Memoria RAM, durante la ejecución del programa:
 - En el stack (pila): si es una variable local.
 - En el heap (montón): si se asigna dinámicamente (por ejemplo, con malloc() en C o new en C++).
 - En la zona de datos globales: si es una variable global o estática.
  
- En registros de la CPU: cuando se usa intensamente en cálculos, el compilador puede asignarla a registros temporales para mejorar el rendimiento.


**Clasificación por tipo**:

| Tipo de Variable       | Ubicación Física                | Organización en Memoria          |
|------------------------|----------------------------------|----------------------------------|
| Variables globales     | Sección `.data` o `.bss`        | Alineadas a tamaño de palabra (4/8 bytes) |
| Variables estáticas    | Sección `.data` (inicializadas) | Mapeadas estáticamente por linker|
| Variables locales      | Stack (registro SP/FP)          | Frame de pila con offsets fijos  |
| Variables dinámicas    | Heap (malloc/new)               | Administrado por allocator (buddy system, slab) |


# FETCH DECODE EXECUTE

## 1. **Fetch (Búsqueda de Instrucción)**
**Qué sucede**:  
El CPU *trae* la siguiente instrucción desde memoria. Es como buscar la siguiente receta en un libro de cocina.

**Detalles técnicos**:
- El **Program Counter (PC)** actúa como "dedo señalador" que indica la dirección de memoria
- La instrucción viaja por el **bus de datos** desde la caché L1i (Instruction Cache) al registro de instrucción
- En x86: El prefetcher ya está buscando las siguientes 16-32 bytes especulativamente

**Ejemplo**:  
`PC = 0x80400000 → Instrucción "ADD R1, R2, R3" cargada`

## 2. **Decode (Decodificación)**
**Qué sucede**:  
El CPU *interpreta* la instrucción. Similar a traducir los pasos de la receta a acciones concretas.

**Proceso interno**:
- La unidad de control **rompe** el opcode en señales de control
- Se identifican los registros fuente/destino (en arquitecturas RISC)
- En CISC (como x86): El decodificador puede generar múltiples µops

**Casos especiales**:
- Instrucciones SIMD activan unidades vectoriales
- Saltos activan el predictor de bifurcación

**Ejemplo**:  
`"ADD R1, R2, R3" → [ALU_OP=ADD, SRC1=R2, SRC2=R3, DEST=R1]`

## 3. **Execute (Ejecución)**
**Qué sucede**:  
El CPU *realiza* la operación. Es el equivalente a mezclar ingredientes según la receta.

**Dónde ocurre**:
- **Operaciones aritméticas**: En la ALU
- **Accesos a memoria**: En la unidad de carga/almacenamiento
- **Saltos**: En la unidad de control de flujo

**Paralelismo real**:
- Múltiples instrucciones pueden ejecutarse simultáneamente (superescalaridad)
- Resultados se escriben en el **Reorder Buffer** (ROB) para mantener el orden lógico

**Ejemplo**:  
`ALU suma los valores de R2 (0x5) y R3 (0x3) → Resultado 0x8`

<img src="https://github.com/user-attachments/assets/282e6d88-da8a-4f19-930a-c7aa43c79988" width="200px" height="150px" />


# INSTRUCCIONES TIPO A Y C

## Instrucciones Tipo A (Las Calculadoras o Aritmetico - Logicas)

**¿Qué hacen?**  
Son como las operaciones básicas de una calculadora, pero trabajando solo con los "cajones - datos " del procesador (los registros).

**Ejemplos cotidianos**:
- `SUMAR R1, R2, R3` ➡️ R1 = R2 + R3
- `MULTIPLICAR R4, R5, R6` ➡️ R4 = R5 × R6

**Características**:
🔹 **Solo usan datos de los registros** (no tocan la memoria)  
🔹 **Tienen 3 partes**: Qué operación + 2 datos fuente + 1 destino  
🔹 **Son rápidas**: Se resuelven en 1 paso del procesador  

**Analogía**:  
Imagina que estás cocinando:
- Los ingredientes ya están en tu mesa de trabajo (registros)
- Los mezclas directamente (operación)
- El resultado lo dejas en otro bowl (registro destino)

## Instrucciones Tipo C (Las Guías Turísticas)

**¿Qué hacen?**  
Deciden "por dónde seguir" en el programa, como un GPS que cambia la ruta.

**Ejemplos comunes**:
- `IR A línea 50` (salto incondicional)
- `SI X=0 IR A línea 30` (salto condicional)
- `LLAMAR a función` (guarda dónde volver)

**Qué pasa internamente**:
1. El CPU "mira" una condición
2. **Predice** qué camino seguir (¡a veces se equivoca!)
3. Continúa trabajando "por si acaso" (ejecución especulativa)


**Analogía**:  
Como leer un "elige tu propia aventura":
- Adivinas qué página seguir
- Si acertaste, ahorraste tiempo
- Si no, debes volver atrás

## 🔍 Comparación Fácil

|              | Tipo A (Calculadora) | Tipo C (GPS) |
|--------------|----------------------|--------------|
| **Uso**      | Hacer cálculos       | Cambiar flujo |
| **Velocidad**| Super rápida         | Depende      |
| **Riesgo**   | Ninguno              | Puede errar  |
| **Ejemplo**  | 3 + 5                | "Si... ve a..." |


## 💡 ¿Por qué importa esto?

1. **Las Tipo A** son el "motor" del programa (hacen el trabajo pesado)
2. **Las Tipo C** son las "decisiones" (hacen el programa dinámico)
3. Juntas permiten desde sumas hasta inteligencia artificial

**Dato curioso**: En tu teléfono ocurren **billones** de estas operaciones cada segundo, casi todas Tipo A, con algunas Tipo C que guían el proceso.

# DECODIFICACION
Este proceso es llamado tambien el traductor de instrucciones 

## Paso 1: Recibir la Instrucción (El Paquete Cerrado)
- La CPU **recibe números binarios** (como `110010101...`) de la memoria
- Estos números son como un "mensaje cifrado" que debe interpretar
- **Ejemplo real**: La secuencia `10110000 01100101` en x86 significa `MOV AL, 65h`

## Paso 2: Romper en Partes (Como Analizar una Receta)
La CPU divide la instrucción en campos clave:

| Parte de la Instrucción | Qué Indica | Ejemplo (ARM) |
|-------------------------|------------|---------------|
| Primeros 4-6 bits       | Tipo de operación (suma, resta, etc.) | `1010` = Suma |
| Siguientes bits         | Registro destino | `001` = Registro R1 |
| Bits intermedios        | Registros fuentes | `010 011` = R2 y R3 |
| Últimos bits            | Información extra | Modo de desplazamiento |

## Paso 3: Activar Circuitos Correctos (Encender las Máquinas Necesarias)
- Cada combinación de bits **enciende señales eléctricas** diferentes
- **Ejemplo visual**:
  ```plaintext
  Instrucción: ADD R1, R2, R3
  Señales activadas:
  - "Usar la ALU" ✅
  - "Modo suma" ✅
  - "Conectar R2 a entrada A" ✅
  - "Conectar R3 a entrada B" ✅
  - "Guardar resultado en R1" ✅

  
  

### *Tabla de fuentes*

| Pagina | Enlace |
|--------------|--------------|
| Amazon Web Services |[AWS](https://aws.amazon.com/what-is/cpu/?utm_source=chatgpt.com)|
|Study Smarter| [ST](https://www.studysmarter.es/resumenes/ciencias-de-la-computacion/organizacion-y-arquitectura-de-computadoras/registros-de-la-cpu/?utm_source=chatgpt.com) |
| HardZone | [HardZone](https://hardzone.es/reportajes/que-es/unidad-control/?utm_source=chatgpt.com)|

