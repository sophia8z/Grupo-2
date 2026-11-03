## Sistema Drones con IA

Proyecto del curso MDS (Grupo 2). Es el sistema que nos asignó el Grupo 1: un ESP32-S3 que hace de puente entre un módulo de visión artificial y la controladora de vuelo (Pixhawk) de un dron.

## Qué hace?

El módulo de IA detecta cosas con la cámara y le manda esos eventos al ESP32-S3. El ESP32-S3 los reenvía a la Pixhawk usando MAVLink v2 y, al mismo tiempo, recibe la telemetría del dron. Si algo falla (se pierde el enlace con la Pixhawk, el módulo de IA deja de responder, la batería baja de un umbral), activa una lógica Fail-Safe. Además levanta un servidor web propio para ver todo en tiempo real desde el navegador.

```
Módulo IA  ──►  ESP32-S3  ◄──►  Pixhawk
                   │
                   ▼
              Web / App
```

La interfaz entre el módulo de IA y el ESP32-S3 todavía está por confirmar con el Grupo 1.

## Equipo

| Integrante | Rol | Épica a cargo |
|---|---|---|
| Integrante 1 | Scrum Master | E1. Ingestión de video por DMA y módulo de IA |
| Integrante 2 | Product Owner | E2. Puente MAVLink y telemetría bidireccional |
| Integrante 3 | Desarrollador 1 | E4. Servidor web y dashboard |
| Integrante 4 | Desarrollador 2 | E3. Fail-Safe y control preventivo |

Las historias de usuario van de HU-01 a HU-10 y están repartidas así: E1 (HU-01, HU-02), E2 (HU-03 a HU-05), E3 (HU-06 a HU-08) y E4 (HU-09, HU-10).

## Cómo trabajamos

Usamos Scrum con 3 sprints de 2 semanas (semanas 11 a 16):

- **Sprint 1:** recepción de datos del módulo de IA, enlace MAVLink con la Pixhawk y configuración base.
- **Sprint 2:** Fail-Safe local, servidor web básico y telemetría en ambos sentidos.
- **Sprint 3:** dashboard completo, pruebas hardware-in-the-loop y cierre.

El backlog y el avance están en la pestaña **Projects** del repositorio. Las prioridades salen de WSJF y los criterios de aceptación de cada tarea están escritos en Gherkin dentro de su Issue.

## Estructura del repositorio

```
firmware/    código del ESP32-S3 (video_ingest, mavlink_bridge, failsafe, web_server)
web/         dashboard (HTML, JS y CSS)
docs/        arquitectura, definición de hecho, actas de sprint, pruebas HIL
tests/       pruebas unitarias y casos HIL
.github/     plantilla de pull requests y CI
```

## Cómo compilar

Necesitas ESP-IDF 5.x o PlatformIO. Con ESP-IDF:

```bash
git clone https://github.com/sophia8z/Grupo-2.git
cd Grupo-2/firmware
idf.py set-target esp32s3
idf.py build
idf.py -p /dev/ttyUSB0 flash monitor
```

Con PlatformIO:

```bash
pio run -e esp32s3
pio run -e esp32s3 -t upload
```

El puerto serie cambia según el computador (en Windows es algo como `COM3`).

## Cómo colaborar

1. Toma un Issue del tablero y pásalo a *En Proceso*.
2. Crea tu rama desde `develop`, por ejemplo `feature/hu-03-mavlink-bridge`.
3. Escribe los commits con prefijos: `feat:`, `fix:`, `docs:` o `test:`.
4. Abre un Pull Request con `Closes #N` en la descripción.
5. Otro integrante lo revisa; con una aprobación se puede hacer el merge.

Nadie hace push directo a `main` ni a `develop`.

## Definición de hecho

Una tarea está terminada cuando compila sin errores, cumple sus criterios de aceptación, tiene sus pruebas, la aprobó otro integrante y la documentación está al día.

## Licencia

MIT.
