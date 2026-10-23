# SPECS — Flor interactiva por gestos con cámara

## 1. Propósito
Experiencia interactiva en el navegador que usa la cámara web y detección de manos en tiempo real para hacer crecer, florecer y marchitar una flor dibujada en Canvas 2D:

- **Semilla inicial** → estado base.
- **Mano abierta detectada** → la flor florece (pétalos se abren).
- **Pellizco detectado** (pulgar e índice juntos) → la flor cambia de color.
- **Puño detectado** → la flor deja caer sus pétalos (con sonido) y regresa a semilla.

Todo se dibuja y anima con Canvas 2D. La interacción se controla con CSS (diseño y transiciones) y JavaScript (lógica y detección).

## 2. Alcance de la interacción

| Estado | Descripción | Gesto / disparador |
|--------|-------------|--------------------|
| Semilla | Solo la semilla visible (círculo café), sin tallo ni pétalos | Inicio / después de puño |
| Tallo | Tallo y hojas crecen gradualmente | Mano abierta (primera etapa) |
| Floración | Pétalos se abren alrededor del centro | Mano abierta (segunda etapa) |
| Cambio de color | Pétalos rotan por una paleta de 8 colores | Pellizco (transición, una vez por gesto) |
| Caída de pétalos | Pétalos caen como partículas con sonido y vuelve a semilla | Puño cerrado |

## 3. Decisiones de arquitectura

### 3.1 Librería de detección de manos
- **p5.js + ml5.js (Handpose)** — seleccionada. p5.js carga desde CDN; ml5.js y TensorFlow.js se sirven localmente desde `libs/` para evitar bloqueos de MIME/CORS.

### 3.2 Formato del proyecto
- **Un solo archivo HTML** — seleccionado. `index.html` con HTML, CSS y JS embebidos; se abre directo en el navegador. Librerías en `libs/`.

### 3.3 Estilo visual de la flor
- **Minimalista / geométrico** — seleccionado. Formas simples, colores planos, transiciones suaves.

### 3.4 Idioma de la interfaz
- **Español** — seleccionado.

## 4. Registro de decisiones

| Decisión | Opción elegida | Fecha |
|----------|----------------|-------|
| Librería de detección de manos | p5.js + ml5.js (Handpose) | |
| Formato del proyecto | Un solo archivo HTML | |
| Estilo visual de la flor | Minimalista / geométrico | |
| Idioma de la interfaz | Español | |

## 5. Requisitos funcionales
RF-01: Acceso a la cámara web y visualización del video.
RF-02: Detección de manos en tiempo real con landmarks de dedos.
RF-03: Reconocimiento de gesto "mano abierta" (dedos extendidos).
RF-04: Reconocimiento de gesto "puño" (dedos doblados).
RF-05: Reconocimiento de gesto "pellizco" (pulgar e índice juntos).
RF-06: Dibujo y animación de flor en Canvas 2D (semilla, tallo, hojas, pétalos, centro).
RF-07: Transiciones visuales entre estados (florecer, cambiar color, caer pétalos, volver a semilla).
RF-08: Partículas al caer pétalos cuando se cierra el puño.
RF-09: Sonido descendente (p5.sound) cuando caen los pétalos.
RF-10: Cambio de color de pétalos (paleta de 8 colores rotando) al hacer pellizco.
RF-11: Feedback visual del estado actual (texto o indicador).

## 6. Criterios de aceptación
- [ ] Abrir el archivo HTML y conceder permiso de cámara.
- [ ] Ver la semilla café en pantalla al inicio.
- [ ] Mostrar mano abierta → ver la flor florecer.
- [ ] Hacer pellizco → ver la flor cambiar de color.
- [ ] Cerrar puño → escuchar sonido, ver pétalos caer y regresar a semilla.
- [ ] Animaciones fluidas sin saltos bruscos.

## 7. Riesgos conocidos
- Permisos de cámara denegados.
- Modelos de ml5.js Handpose bloqueados por MIME/CORS en CDNs públicos (resuelto sirviendo `libs/` localmente).
- Rendimiento en dispositivos móviles con cámara y Canvas simultáneos.
- Detección inconsistente de gestos según iluminación.
- Falsos positivos de pellizco si el umbral de distancia (40 px) no se ajusta a la distancia de la mano.

## 10. Implementación
El código completo y listo para usar está en `index.html` (un solo archivo HTML con HTML, CSS y JS embebidos). Abrilo en el navegador, concedé permiso de cámara y empezá a interactuar.

Decisiones tomadas:
- Detector: p5.js + ml5.js (Handpose)
- Formato: Un solo archivo HTML
- Estilo: Minimalista / geométrico
- Idioma: Español
