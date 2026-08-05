# Dashboard de cupos disponibles

Primera versión de interfaz para controlar la agenda de agosto de 2026. Abra `index.html` manteniendo `data.js` en la misma carpeta.

## Filtros dependientes

Los selectores siguen este orden: **Estado del cupo → Fecha → Estamento → Profesional → Sector → Tipo de atención**. Cada selector sólo ofrece valores compatibles con la selección que lo antecede. La fecha queda aplicada en **Desde hoy en adelante** y se recalcula al abrir el dashboard, por lo que no muestra días ya transcurridos. Por ejemplo, después de elegir **Médico** en Estamento, el selector Profesional muestra únicamente médicos.

**Tipo de atención** usa casillas de selección múltiple: puede marcar una o varias prestaciones; el tablero combinará los cupos que correspondan a cualquiera de ellas. Use el buscador sobre las casillas para encontrar una prestación rápidamente.

## Indicadores incluidos

- Cupos totales, citados, disponibles y bloqueados.
- Diagnóstico rápido de disponibilidad con semáforo, proporción de cupos abiertos, cupos abiertos de la fecha actual y próxima mayor oportunidad.
- Ocupación habilitada: `citados / (citados + disponibles)`.
- Disponibilidad diaria por cupos abiertos, para priorizar días de difusión o captación.
- Cupos abiertos por estamento, profesional, horario y sector.
- Alertas de gestión y descarga de todo el detalle filtrado en Excel (`.xlsx`).

## Conectar Google Sheets

1. Cargue los datos operativos en una pestaña que tenga **la primera fila como encabezado** y estas columnas: `FECHA`, `PROFESIONAL`, `TIPO DE ATENCION`, `ESPECIALIDAD`, `INSTRUMENTO`, `ESTADO CUPO`, `SECTOR`, `TOTAL CUPOS`.
2. Publique únicamente esa pestaña como CSV o implemente una capa autenticada acorde a la política institucional.
3. En `index.html`, reemplace el valor vacío de `GOOGLE_SHEETS_CSV_URL` por la URL CSV publicada.
4. Antes de publicar en GitHub, quite `data.js` o use un repositorio privado: el archivo contiene nombres de profesionales y la planilla origen advierte sobre tratamiento de información sensible.

## Publicar con GitHub Desktop y VS Code

1. Abra **GitHub Desktop** y elija **File → Add local repository**. Seleccione esta carpeta: `outputs/dashboard-cupos-agosto`.
2. Presione **Open in Visual Studio Code**. En `config.js`, pegue la URL CSV publicada de Google Sheets en `googleSheetsCsvUrl`.
3. Compruebe el dashboard localmente y verifique que `data.js` no aparezca entre los archivos a publicar: está excluido en `.gitignore`.
4. En GitHub Desktop, escriba un resumen de cambios y use **Commit to main**. Luego, elija **Publish repository**.
5. En el repositorio de GitHub, vaya a **Settings → Pages**, seleccione **Deploy from a branch**, y elija `main` y la carpeta `/(root)`.

Para una publicación pública, la pestaña de Google Sheets también debe ser pública; eso expone los datos que contiene. Mientras se defina la política de privacidad institucional, la alternativa prudente es mantener el repositorio privado y no publicar la hoja de datos.

La fuente actual describe agenda; no permite medir atenciones efectivamente realizadas ni inasistencias.
