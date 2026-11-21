# Sistema Drones con IA

Proyecto final de Metodologías de Desarrollo de Software (Grupo 2). Un ESP32-S3 conecta un módulo de visión artificial con la controladora de vuelo (Pixhawk) de un dron.

## Qué hace

El módulo de IA detecta rostros con la cámara y envía cada detección por UART al ESP32-S3. El ESP32-S3 valida la trama, descarta las de baja confianza, las reenvía a la Pixhawk por MAVLink y activa una alerta (GPIO) si la confianza es alta. Si el módulo de IA deja de responder, un Fail-Safe lo reinicia y avisa.

```
Cámara + Módulo IA --UART--> ESP32-S3 --MAVLink--> Pixhawk
 (Edge Impulse)                 |
                                +--> GPIO (alerta)
```

## Alcance

- **Incluido:** modelo de detección (Roboflow + Edge Impulse), ingesta UART con CRC16, puente MAVLink, alerta GPIO y Fail-Safe.
- **Backlog futuro:** servidor web, dashboard y pruebas HIL. Se dejaron fuera por tiempo y equipo (ver bitácora).

## Equipo

| Integrante   | Rol                      | Estado   | Responsabilidad actual |
| ------------ | ------------------------ | -------- | ---------------------- |
| Integrante 2 | Product Owner  | Activo | Módulo de IA (Roboflow + Edge Impulse), documentación y evidencias |
| Integrante 4 | Desarrollador 2        | Activo   | Firmware ESP32-S3: ingesta, MAVLink, alerta y Fail-Safe |

## Historial del equipo

| Integrante   | Rol original    | Estado   | Trabajo original | Qué pasó con ese trabajo |
| ------------ | --------------- | -------- | ---------------- | ------------------------ |
| Integrante 1 | Scrum Master    | Retirado (20/11/26) | E1. Ingestión DMA y módulo de IA | Reasignada al Desarrollador 2 |
| Integrante 3 | Desarrollador 1 | Retirado (20/11/26) | E3. Fail-Safe y control preventivo | Reasignada al Desarrollador 2 (HIL pasa al backlog futuro) |

## Cómo trabajamos

Scrum con 3 sprints cortos y un tablero en **Projects**. Cada tarea es un Issue con sus criterios de aceptación; se trabaja en ramas y se une con Pull Request revisado por el otro integrante. Una tarea está hecha cuando funciona, cumple sus criterios y tiene evidencia en `evidencias/`.

| Sprint | Objetivo | Estado |
|---|---|---|
| 1 | Repo, modelo de IA, recepción UART | Pendiente |
| 2 | MAVLink, alerta GPIO, Fail-Safe | Pendiente |
| 3 | Pruebas, informe y demo | Pendiente |

## Estructura

```
firmware/    código del ESP32-S3
ia/          modelo y capturas de Edge Impulse
docs/        trama UART, arquitectura, actas
evidencias/  fotos, capturas, video, pruebas
```

## Bitácora

| Fecha | Qué pasó | Qué aprendimos |
|---|---|---|
| 2026-11-03 | Backlog inicial con 4 integrantes y 3 sprints de 2 semanas | Planificamos para un equipo completo |
| 2026-11-21 | Se retiran 2 integrantes; reducimos el alcance y sumamos el módulo de IA | Priorizar lo esencial y adaptar el plan al equipo real |

## Licencia

MIT
