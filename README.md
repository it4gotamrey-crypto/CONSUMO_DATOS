# Consumo v1.7 · sin internet, Excel y reporte editable

[**Descargar para Android (.zip)**](https://github.com/it4gotamrey-crypto/CONSUMO_DATOS/raw/refs/heads/entrega-consumo-permisos/entregas/consumo-sin-internet.zip)

Un único HTML local, sin usuarios propios y sin servidor. [Guía completa](USO_SIN_INTERNET.md).

## Vista previa antes de imprimir

**Imprimir reporte** abre una vista editable con las páginas que se imprimirán. Elige solo gráficas, solo tablas o ambas, activa el detalle de capturas y mueve/redimensiona las gráficas. Ajusta ancho, alto, orden y orientación A4. La selección puede ser distinta para cada bloque. Las tablas largas repiten encabezados al dividirse por páginas.

Al finalizar, pulsa **Imprimir / Guardar PDF**. En el navegador elige el mismo papel y orientación, escala 100% y desactiva los encabezados y pies del navegador.

[Ver la vista previa](entregas/vista-previa-impresion.png) · [PDF de ejemplo con datos ficticios](entregas/reporte-ejemplo.pdf)

## Abrir en Android

1. Descarga el ZIP y extráelo en **Archivos / Descargas**.
2. Abre **consumo-sin-internet.html** con un navegador compatible con HTML local; prueba Chrome si tu teléfono lo ofrece y ejecuta la aplicación correctamente.
3. Captura los datos o importa tu respaldo JSON/Excel.

La descarga comienza vacía para no publicar capturas privadas. Antes de cambiar el HTML anterior, conserva un **respaldo JSON** y comprueba su restauración. Los datos permanecen en ese dispositivo y navegador.

## Descargar Excel

Pulsa **Descargar Excel** en **Respaldo y exportación** o **Capturas mensuales**. El `.xlsx` contiene ocho hojas de detalles y resúmenes, respeta los filtros y excluye pendientes de los totales validados. Funciona sin internet.

Las opciones **Guardar panel**, **Copiar HTML** y **Descargar panel** siguen eliminadas. Un HTML local continúa siendo un archivo copiable/modificable; los datos oficiales se protegerán en el servidor cuando se integre a Artron.

## Integración final

Se reutilizarán el login y los permisos existentes de Artron. La conexión real con su API está pendiente. Ver [INTEGRACION_LOGIN_ARTRON.md](INTEGRACION_LOGIN_ARTRON.md).

Se conserva [el servidor independiente anterior](entregas/consumo-artron-con-permisos.zip) y [su guía](INSTALACION_SERVIDOR.md) como alternativa técnica. No son necesarios para usar el HTML sin red y no corresponden al mecanismo de acceso elegido para Artron.
