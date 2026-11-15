# logSguarDian

## Descripción

logSguarDian es un middleware RASP para Node.js/Express que detecta y bloquea en tiempo real inyección SQL, XSS, Path Traversal y Command Injection. Utiliza un modelo híbrido de Machine Learning (Random Forest + Isolation Forest) entrenado sobre ~380,000 solicitudes HTTP etiquetadas y exportado a ONNX, que se ejecuta en `worker_threads` para no bloquear el Event Loop.

Está pensado para pequeñas y medianas empresas que no cuentan con un equipo de seguridad dedicado: se instala con una línea de código y no requiere desplegar infraestructura adicional (WAF, IDS). Funciona en modo `block` (responde HTTP 403) o `monitor` (solo registra). Incluye una CLI para configuración, reportes y webhooks.

El paquete está publicado en npm como [`logsguardian`](https://www.npmjs.com/package/logsguardian).

## Tecnologías Utilizadas

- Node.js y TypeScript
- Express
- ONNX Runtime (`onnxruntime-node`)
- Python, scikit-learn y Jupyter (entrenamiento de modelos)
- SQLite (`better-sqlite3`)
- pnpm (monorepo con workspaces)
- Jest y Supertest (pruebas)
- ModSecurity + OWASP CRS (evaluación comparativa)

## Requisitos Previos

- Node.js v20 o superior
- pnpm v9 o superior
- Python 3.10+ (solo para reentrenar los modelos; no es necesario para ejecutar la librería)

## Instalación

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/Diegoval-Dev/2026-22309-valenzuela-palacios-diego-pablo.git
   cd 2026-22309-valenzuela-palacios-diego-pablo
   ```
2. Instalar dependencias:
   ```bash
   cd src
   pnpm install
   ```
3. Configurar variables de entorno (opcional, todas tienen valores por defecto):
   ```bash
   cp .env.example .env
   ```
4. Compilar y ejecutar las pruebas:
   ```bash
   pnpm build
   pnpm test
   pnpm test:e2e
   ```

### Uso de la librería

```js
const { logsguardian } = require('logsguardian');
app.use(logsguardian({ mode: 'block' }));
```

Para generar el archivo de configuración con la CLI:

```bash
npx logsguardian config init
```

La referencia de comandos está en [`src/docs/commands.md`](src/docs/commands.md) y la arquitectura en [`src/docs/architecture.md`](src/docs/architecture.md).

## Capturas

Las capturas de pantalla del sistema se encuentran en [`/capturas`](capturas) (12 imágenes: sitio web, paquete en npm, CLI, pruebas, métricas de los modelos y resultados de la evaluación).

## Demo

El video demostrativo se encuentra en [`/demo/demo.mp4`](demo/demo.mp4)

## Documentación

El informe final del proyecto está disponible en [`/docs/informe_final.pdf`](docs/informe_final.pdf)

El consentimiento de uso de foto y video firmado se encuentra en [`/docs/consentimiento_firmado.pdf`](docs/consentimiento_firmado.pdf)

## Autores

- Diego Pablo Valenzuela Palacios - 22309

La librería fue desarrollada junto con Sebastian Huertas.

Universidad del Valle de Guatemala, 2026.

## Licencia

MIT
