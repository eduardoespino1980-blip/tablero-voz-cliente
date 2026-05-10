# Tablero Voz del Cliente — Hivimar Industrial

Tablero estático autocontenido con cumplimiento de entregas, pedidos PRIME, retiros por agente y ventas YTD para los 4 clientes MPV del segmento Industrial.

## Acceso

URL pública: `https://<tu-usuario>.github.io/<repo>/tablero_voz_cliente.html`

Contraseña: solicitar al administrador.

## Cómo desplegarlo en GitHub Pages

1. Crear el repositorio en GitHub (público, gratis).
2. Subir los archivos:
   - `tablero_voz_cliente.html`
   - `logo_hivimar_industrial.png`
   - (opcional) `README.md`
3. En el repo: **Settings → Pages → Source → Branch `main` → Save**.
4. Esperar 1–2 minutos. Tu URL queda en `https://<usuario>.github.io/<repo>/tablero_voz_cliente.html`.

## Cómo embeberlo en PowerPoint

**Opción recomendada (Office 365):**

1. Insertar → Mis complementos → Buscar "Web Viewer" → Agregar.
2. Pegar la URL de GitHub Pages.
3. El tablero queda interactivo durante la presentación (modo slideshow). Requiere internet.

**Opción simple (cualquier PowerPoint):**

1. Capturar pantalla del tablero, insertar como imagen.
2. Click derecho → Hipervínculo → pegar la URL.
3. En presentación, click abre el tablero en el navegador.

## Cómo regenerar los datos

Estos scripts están en la carpeta del proyecto (no se suben al repo público):

| Script | Qué hace |
|---|---|
| `extraer_agente_industrial.py` | Pagina Hivitrack, filtra LN=1100, identifica RETIRA AGENTE → `datos_agente_industrial.json` |
| `extraer_ventas_ytd.py` | Lee `ventas_enriquecido.csv` (SGI 2.0), calcula YTD por cliente y categorías → `datos_ventas_ytd.json` |
| `extraer_oportunidades.py` | Lee `oportunidades_enriquecido.csv` (Odoo) → `datos_oportunidades.json` |
| `generar_tablero.py` | Combina todos los JSON + logo y produce `tablero_voz_cliente.html` |

Flujo de actualización mensual:

```
python extraer_agente_industrial.py
python extraer_ventas_ytd.py
python extraer_oportunidades.py
python generar_tablero.py
# Subir tablero_voz_cliente.html a GitHub
```

## Estructura

```
Tablero Voz del Cliente/
├── tablero_voz_cliente.html   ← el tablero (este se sube a GitHub)
├── logo_hivimar_industrial.png ← logo (se sube a GitHub)
├── README.md                   ← este archivo
├── .gitignore                  ← excluye .env y datos detallados
│
├── generar_tablero.py          ← generador (NO subir si tiene rutas locales)
├── extraer_*.py                ← extractores (NO subir, contienen rutas locales)
├── hivitrack_client.py         ← cliente API (NO subir, no tiene secretos pero no aporta)
├── .env                        ← credenciales (NUNCA subir)
└── datos_*.json                ← datos crudos (subir solo si OK con privacidad)
```

## Privacidad

El tablero es un HTML estático con todos los datos embebidos. La contraseña solo bloquea la interfaz visual; el código fuente (con datos) es visible para quien tenga la URL. Para mayor seguridad, considerar:

- Repositorio privado (requiere GitHub Pro/Team)
- Servidor interno con autenticación real
- Mover datos a JSON cargado tras autenticación

## Soporte

Mantenimiento y dudas: equipo Hivimar Industrial.
