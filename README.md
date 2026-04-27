# Board Game Timer

Aplicación web (PWA) para gestionar turnos en juegos de mesa con reloj individual por jugador.

## Características

- Configuración de **2 a 8 jugadores**.
- Tiempo inicial por jugador configurable.
- **Incremento por turno** configurable.
- Edición de nombre, color y orden de jugadores antes de iniciar.
- Guardado de **grupos de jugadores** en `localStorage` (crear, actualizar, cargar y borrar).
- Modo de partida con:
  - jugador activo resaltado,
  - pase de turno con un toque,
  - contador de agotamientos de tiempo,
  - historial reciente de tiempos agotados.
- Panel de pausa para ajustar el tiempo base y el incremento durante la partida.
- Botón de pantalla completa.
- Solicitud de **Wake Lock** (si el dispositivo/navegador lo permite) para evitar que la pantalla se apague durante la partida.
- Soporte **offline** mediante Service Worker.
- Instalación como app gracias al `manifest.webmanifest`.

## Estructura del proyecto

- `board_game_timer.html`: aplicación principal (UI + lógica en un único archivo).
- `index.html`: redirección a la aplicación principal.
- `sw.js`: Service Worker para caché de app shell y recursos.
- `manifest.webmanifest`: configuración PWA.
- `icon.svg` / `icon-maskable.svg`: iconos de la aplicación.

## Requisitos

No requiere dependencias ni build step. Solo necesitas un navegador moderno.

> Nota: para que el Service Worker funcione correctamente, abre la app desde `http://localhost` (o HTTPS), no con `file://`.

## Ejecución local

Desde la raíz del proyecto puedes levantar un servidor estático, por ejemplo:

```bash
python3 -m http.server 8080
```

Luego abre:

- `http://localhost:8080/` (redirige a la app), o
- `http://localhost:8080/board_game_timer.html`

## Uso rápido

1. Selecciona número de jugadores.
2. Ajusta tiempo inicial e incremento.
3. Edita nombres, colores y orden.
4. (Opcional) Guarda el grupo de jugadores.
5. Pulsa **Iniciar**.
6. Durante la partida, toca la tarjeta del jugador activo para pasar turno.
7. Usa **Pausar/Ajustes** para modificar parámetros o **Salir** para volver a la configuración.

## Datos persistentes

Los grupos de jugadores se guardan en el navegador con `localStorage` bajo la clave:

- `boardGameTimerSavedGroups`

Si borras los datos del sitio en el navegador, también se eliminarán estos grupos.

## Compatibilidad

La app está orientada a móviles en vertical, pero funciona también en escritorio.
Algunas funciones dependen del navegador:

- Wake Lock: solo en navegadores compatibles.
- Pantalla completa: puede variar según dispositivo/permisos.
- Instalación PWA/offline: requiere soporte de Service Worker + manifest.
