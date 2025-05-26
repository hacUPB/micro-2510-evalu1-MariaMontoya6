# MAPA DE MEMORIA Y ARQUITECTURA

## ¿Mapa de memoria?

El **mapa de memoria** de un microprocesador es una representación organizada de cómo se distribuye el espacio de memoria accesible por el CPU. 

**Características principales:**
- Define las direcciones de memoria asignadas a diferentes componentes (RAM, ROM, periféricos, etc.)
- Establece los rangos de direcciones para cada dispositivo conectado al bus del sistema
- Puede ser fijo o configurable dependiendo de la arquitectura

**Funciones principales:**
1. Permite al procesador acceder a dispositivos y memoria de forma ordenada
2. Evita conflictos de direcciones entre componentes
3. Facilita la gestión de recursos del sistema
4. Define áreas específicas para código, datos y dispositivos de E/S

<img src="https://github.com/user-attachments/assets/3dff561a-0e98-4665-beed-07b23439f903" width="300px" height="300px" />

1. **¿Cuántos pines del bus de direcciones del MC6802 se utilizan en esta conexión? ¿Cuáles son los nombres utilizados para representarlos?**  
   - **Respuesta:**  
     Se utilizan **11 pines** del bus de direcciones.  
     Los nombres utilizados son **A0 a A10**.

2. **¿De qué valor es la memoria total de almacenamiento del MC6846? Incluye los cálculos que realizaste.**  
   - **Respuesta:**  
     El MC6846 contiene **2 KBytes de ROM**.  
     **Cálculo:**  
     1 KByte = 1024 bytes → 2 KBytes = 2 × 1024 = **2048 bytes**.  
     La memoria total es de **2048 bytes (2 KBytes)**.

3. **¿Cuántos bits ocupa cada dato al que se puede acceder en la memoria MC6846? ¿Cómo lo dedujiste?**  
   - **Respuesta:**  
     Cada dato ocupa **8 bits**.  
     **Deducción:**  
     El bus de datos está etiquetado como **D0–D7** (8 líneas), lo que indica que cada transacción es de **8 bits**.

# TIPOS DE ARQUITECTURA 

## Arquitectura von Neumann
- **Característica principal:** Memoria unificada para datos e instrucciones
- **Ventajas:**
  - Diseño más simple
  - Flexibilidad en el uso de memoria
  - Menor costo de implementación
- **Desventajas:**
  - Cuello de botella en el bus (efecto von Neumann)
  - Menor eficiencia en procesamiento paralelo

## Arquitectura Harvard
- **Característica principal:** Memorias separadas para datos e instrucciones
- **Ventajas:**
  - Mayor velocidad (acceso paralelo a datos e instrucciones)
  - Mejor seguridad (protección de código)
  - Optimización para pipelines
- **Desventajas:**
  - Mayor complejidad
  - Coste más elevado
  - Menor flexibilidad
 
<img src="https://github.com/user-attachments/assets/c662877c-c597-4ab9-9abf-77a1ae41da52" width="450px" height="400px" />

**Nota:** Muchos sistemas modernos usan arquitecturas híbridas que combinan aspectos de ambos modelos.

# ARQUITECTURA CISC Y RISC 

### Arquitectura CISC (Complex Instruction Set Computer)
- **Características:**
  - Instrucciones complejas y variadas
  - Cada instrucción puede realizar múltiples operaciones
  - Modos de direccionamiento complejos
  - Microcódigo para implementar instrucciones
  - Menos registros de propósito general
- **Ventajas:**
  - Código más compacto
  - Facilita la programación en ensamblador
  - Bueno para aplicaciones específicas

### Arquitectura RISC (Reduced Instruction Set Computer)
- **Características:**
  - Juego de instrucciones reducido y simple
  - Instrucciones de tamaño fijo y ejecución en un ciclo de reloj
  - Mayor número de registros de propósito general
  - Filosofía "load-store" (sólo load/store acceden a memoria)
- **Ventajas:**
  - Mayor velocidad de ejecución
  - Más eficiencia energética
  - Mejor para pipelines
  - Facilita la optimización por compiladores

**Evolución:** Muchos diseños modernos son RISC-like internamente pero con frontends CISC (ej: x86-64).

# Análisis sobre las arquitecturas de microprocesadores:

1. **Convergencia tecnológica:** Observamos una tendencia hacia arquitecturas híbridas que combinan lo mejor de cada enfoque. Por ejemplo:
   - Procesadores x86 (externamente CISC) con núcleos RISC internos
   - Arquitecturas Harvard modificadas para ciertos niveles de caché

2. **Contexto de aplicación:** La elección de arquitectura depende del uso:
   - **Embedded/IoT:** Harvard y RISC dominan (ARM, AVR)
   - **Computación general:** Von Neumann con extensiones CISC siguen siendo relevantes
   - **High Performance:** Combinaciones complejas con múltiples buses

3. **Innovación constante:** Nuevos paradigmas como:
   - Arquitecturas aceleradoras (GPUs, TPUs)
   - Procesadores cuánticos con modelos radicalmente diferentes
   - Arquitecturas neuromórficas

4. **Eficiencia energética:** Se ha convertido en un driver principal de diseño, favoreciendo enfoques RISC en muchos casos.

**Conclusión:** No existe una arquitectura "mejor" universalmente, sino soluciones optimizadas para diferentes necesidades. La diversidad arquitectónica actual permite elegir la mejor herramienta para cada tarea específica, y seguirá evolucionando para satisfacer nuevas demandas computacionales.

<img src="https://github.com/user-attachments/assets/0fd9272b-6386-4bb8-b2d0-aaa9433e62ba" width="300px" height="150px" />


