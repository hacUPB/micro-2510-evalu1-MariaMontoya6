[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/SSOqGLPb)
# Unidad No. 2
# COMPONENES DE UN PROCESADOR Y SU FUNCIONAMIENTO 
## Información del estudiante  
### Mariajose Montoya Cruz
### 507335

# 🖥️ Componentes de un Procesador - Actividad 1

Este repositorio contiene el desarrollo de la **Actividad 1** de la materia **Microprocesadores**, cuyo objetivo es analizar y comprender los principales componentes que conforman un procesador.

## 📚 Objetivo de la Actividad

Comprender la función y la interacción de cada componente dentro del procesador, desarrollando una base teórica sólida para el estudio de arquitecturas computacionales.


## 📂 Estructura del Repositorio

### 📁 Conceptos Iniciales

[Ver conceptos iniciales ](Act_1_Componentes_de_un_procesador/Conceptos_iniciales.md)

Este contine el archivo donde se describen los siguientes componentes clave de un procesador:

- **Unidad de Control (UC)**  
  Coordina y dirige todas las operaciones del procesador, desde la búsqueda y decodificación de instrucciones hasta su ejecución.
- **Unidad Aritmético-Lógica (ALU)**  
  Se encarga de realizar operaciones matemáticas (suma, resta, etc.) y lógicas (comparaciones, operaciones booleanas).
- **Registros**  
  Pequeñas memorias internas que almacenan datos temporales y resultados intermedios.
- **Memoria Caché**  
  Almacena datos e instrucciones de uso frecuente para mejorar el rendimiento del sistema.
- **Buses**  
  Canales por los que se transfieren datos, direcciones y señales de control entre los distintos componentes del sistema.

### 📁 ISA
[Ver ISA](Act_1_Componentes_de_un_procesador/ISA.md)

Este documento explica los fundamentos de la arquitectura ARM, especialmente orientado al Cortex-M4 y su uso en sistemas embebidos.

Puntos clave:
- Arquitectura RISC: Conjunto de instrucciones reducido, eficiente y fácil de implementar.
- Popular en móviles: Por su bajo consumo y buen rendimiento. Thumb-2: Instrucciones de 16 y 32 bits que reducen tamaño de código sin afectar velocidad.
- Registros: R0–R12 (generales), SP (R13), LR (R14), PC (R15), xPSR (estado).
- Modos: Thread (normal) e Interrupt (excepciones).
- Cortex-M4: Soporte DSP, FPU opcional, pipeline de 3 etapas y bajo consumo.

🛠️ Código en ensamblador:
Incluye ejemplos con instrucciones como MOV, CMP, B, desplazamientos lógicos y aritméticos, y estructuras condicionales (if, while, etc.).

### 📁 MAPA DE MEMORIA
[Ver mapa de memoria](Act_1_Componentes_de_un_procesador/Mapa_de_Memoria.md)

Este apartado explora cómo se organiza la memoria en microprocesadores y las principales arquitecturas usadas en sistemas computacionales.

🗺️ Mapa de Memoria
- Representa cómo el procesador accede a RAM, ROM y periféricos.
- En el MC6802 se usan 11 líneas de dirección (A0–A10).
- El MC6846 tiene 2 KB de ROM y acceso a datos de 8 bits (D0–D7).

🏛️ Tipos de Arquitectura

-Von Neumann: Memoria compartida para datos e instrucciones (simple pero con cuello de botella).
Harvard: Memorias separadas (más rápida y segura, pero compleja).

CISC vs. RISC:

- CISC: Instrucciones complejas, código compacto.
- RISC: Instrucciones simples, ejecución eficiente y energética.

🌐 Tendencias
- Uso de arquitecturas híbridas (ej. Harvard modificada, CISC con núcleo RISC).
- Elección de arquitectura depende del contexto: IoT, computación general, HPC, etc.
- La eficiencia energética impulsa la adopción de RISC en muchos entornos modernos.


  


