# CLAUDE.md — Dashboards de Calidad Manufactura (lives-dashboards-calidad)

Las reglas generales de trabajo están en el repo privado `lives-instrucciones` (CLAUDE.md). Este archivo solo describe esta herramienta.

## Qué hace
Cinco dashboards de solo lectura de las auditorías de calidad, con el mismo motor (Chart.js): KPIs de % de rechazo y % de aprobación, vista Semana/Mes/Año, tendencia, defectos principales y desempeño. Ninguno registra nada.
- `lineas/dashboard-lineas.html` — Auditoría en Líneas de Costura (tipo LINEAS): por línea, inspector y cliente; líneas "fusionadas" o "reales".
- `empaque/dashboard-empaque.html` — Auditoría en Empaque (tipo EMPAQUE): por auditora, cliente y taller; incluye cajas y % de defecto (prendas defectuosas ÷ revisadas).
- `inspeccion/dashboard-inspeccion.html` — Auditoría de Servicio de Inspección (tipo SERVINSP): por inspector y cliente.
- `cliente/dashboard-cliente.html` — Auditoría de Cliente (tipo CLIENTE): por cliente, ranking del año. Versión algo anterior del motor.
- `final/dashboard-final.html` — Auditoría Final Interna y Talleres: KPIs LIVES y TALLERES, mejor y peor taller, defectos (sobre muestra AQL) y derivados (sobre lote completo) por separado, reprocesos y licencias. Es el más grande.
- Lineas, empaque e inspección son casi copias: solo cambian la configuración (`CFG`), el tipo y algunas columnas.
- Todos traen incrustado el histórico 2025 y conservan funciones heredadas: carga manual de Excel, "Exportar para enviar" (HTML descargable) e "Imprimir A4". Excel: el del bloque LIVES.
- Ya retiradas: Segundas Interno y Control de datos (este último pasó a tarea programada).

## Base de datos (Supabase lives-datos)
- Lineas, empaque, inspección y cliente leen la vista `publico_auditorias` filtrada por `tipo_auditoria` (sale de las tablas `auditorias` y `ops`).
- Final lee `publico_final` (de `auditorias` y `ops`) y `publico_final_detalle` (detalle de defectos y derivados, solo capturas EN VIVO).
- Todos leen `publico_estado_copia` (de `sync_estado`).
- Las auditorías se registran en `lives-registro-auditorias` y `lives-auditoria-final`.
- No usa funciones propias ni Storage.

## Quién la usa
Según las entradas por el portal de los últimos 30 días al 21/10/2026: 8 personas, sobre todo gerencias (General, Producción, Planeamiento), supervisor de planta, supervisora de Top Sample y digitadoras de Calidad.

## Quién puede ver
Solo lectura; no tiene permisos propios.

## Pendientes vistos al escribir esto (21/10/2026)
- Quedan comentarios que mencionan Apps Script y una constante de hoja de Google sin uso en `final`.
- Errata en empaque: "Auditoraes que más lo detectan".
