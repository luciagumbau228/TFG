# Célula de plaetizado - Software de control con KUKA KRC5

Proyecto desarrollado como Trabajo Fin de Grado en Inteligencia Robótica (Universitat Jaume I).

El proyecto consiste en la migración, rediseño y optimización del software de control de una célula industrial de paletizado de cajas desde una plataforma Fanuc a un controlador KUKA KRC5, utilizando KRL (KUKA Robot Language) y técnicas de Virtual Commissioning mediante un gemelo digital.

La validación se ha realizado íntegramente en un entorno virtual basado en iiQWorks.Sim, permitiendo verificar la lógica de control, las trayectorias del robot y los tiempos de ciclo antes de una posible puesta en marcha en planta.

## Objetivos del proyecto
* Migrar la lógica de control desde una plataforma Fanuc a KUKA KRC5.
* Desarrollar una arquitectura modular y mantenible en KRL.
* Implementar la secuenciación automática del proceso de paletizado.
* Integrar la gestión de señales industriales y actuadores neumáticos.
* Optimizar trayectorias mediante movimientos continuos tipo Spline.
* Validar el sistema mediante un gemelo digital.
## Tecnologías utilizadas
* KUKA KRC5
* KUKA Robot Language (KRL)
* iiQWorks.Sim 
* Virtual Commissioning
* GitHub
## Caractterísticas principales
### Arquitectura modular
El software se estructura en módulos independientes que separan lógica de producción, planificación de trayectorias y gestión de señales:* Gestión del ciclo principal.
* Control del ciclo principal de producción
* Secuenciación mediante máquina de estados
* Rutinas de recogida y dejada
* Gestión de rechazos
* Procedimientos de mantenimiento y reinicio
* Simulación de señales y sensores mediante SPS.SUB
### Movimientos optimizados
Se han utilizado movimientos basados en tecnología Spline:
* SPTP
* SLIN
frente a la programación clásica mediante:
* PTP
* LIN
permitiendo reducir paradas intermedias y mejorar la continuidad del movimiento.
### Gestión de eventos en tiempo real
El sistema integra:
* Interrupciones (INTERRUPT)
* Triggers en trayectoria (TRIGGER)
* Temporizadores ($TIMER[])
* Señales de E/S 
* Comunicación con PLC mediante señales de sincronización
### Integración de periféricos industriales

La célula está diseñada para integrarse con una herramienta neumática multifunción controlada mediante una isla de electroválvulas SMC. 

Durante el desarrollo del gemelo digital, las señales de actuación y realimentación de la herramienta fueron simuladas mediante E/S virtuales para permitir la validación completa de la lógica de control.

La arquitectura de software ha sido desarrollada considerando una futura integración mediante PROFINET con una isla de válvulas SMC EX600 y la sensórica asociada, manteniendo la correspondencia entre señales lógicas y dispositivos físicos de planta.
## Validación mediante gemelo digital
El sistema fue validado en entorno virtual utilizando el siulador iiQWorks.sim, incluyendo:
* Verificación de trayectorias sin colisiones
* Validación de alcance y singularidades
* Validación de sincronización de señales
* Simulación completa del flujo de producción
* Evaluación del comportamiento de la pinza y los actuadores neumáticos.
* Análisis de tiempos de ciclo

<img width="1628" height="927" alt="Captura de pantalla 2026-05-03 152541" src="https://github.com/user-attachments/assets/570d49bf-6fe6-48d1-9990-e50b32a41972" />
El elemento terminal mostrado en la simulación ha sido simplificado para preservar información confidencial del sistema real, manteniendo la misma funcionalidad y puntos de conexión.

## Estructura del repositorio

```text
KRC/
├── R1/
│   ├── Program/
│   │   ├── RSR0001.src
│   │   ├── Paletiza.src
│   │   ├── Calc_Mosaico.src
│   │   ├── Calc_Rec.src
│   │   ├── Recoger.src
│   │   ├── Dejar.src
│   │   ├── Rechazo.src
│   │   └── Mantenimiento.src
│   │
│   └── System/
|       ├── $CONFIG.DAT
│       └── SPS.SUB
│
└── STEU/
    └── MADA
```
## Resultados obtenidos
* Migración completa de la aplicación de control Fanuc → KUKA KRC5
* Validación funcional del sistema en entorno virtual
* Integración de la lógica de producción y control de periféricos
* Optimización de trayectorias mediante movimientos Spline
* Arquitectura modular escalable y mantenible
* Software preparado para su integración y validación sobre hardware industrial real.
