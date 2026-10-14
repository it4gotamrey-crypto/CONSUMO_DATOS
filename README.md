# Consumo v1.6.1 · sin internet y con descarga Excel

**Versión elegida para probar ahora:** un HTML local, sin usuarios propios y sin servidor.

[**Descargar para Android (.zip)**](https://github.com/it4gotamrey-crypto/CONSUMO_DATOS/raw/refs/heads/entrega-consumo-permisos/entregas/consumo-sin-internet.zip)

[Descargar solamente el HTML](https://github.com/it4gotamrey-crypto/CONSUMO_DATOS/raw/refs/heads/entrega-consumo-permisos/entregas/consumo-sin-internet.html)

## Versión 1.6.1

Se eliminaron **Guardar panel**, **Copiar HTML** y **Descargar panel** de la aplicación, incluida la función que mostraba el código completo. Se conservan importar Excel, respaldar/restaurar JSON, descargar Excel/CSV e imprimir. Esta eliminación es una mejora de la interfaz; un archivo HTML local continúa siendo copiable y modificable como archivo.

## Descargar Excel

En **Respaldar y exportar**, pulsa **Descargar Excel**. También aparece en **Capturas mensuales**. El archivo `.xlsx` incluye ocho hojas con las capturas y los resúmenes por aplicación, usuario, departamento y período. Funciona sin internet, respeta los filtros y excluye pendientes de los totales validados.

Antes de cambiar tu HTML por esta versión, crea un **respaldo JSON** del anterior. Si el navegador abre el archivo actualizado como una copia nueva, restaura ese JSON para conservar las capturas.

## Abrir en Android

1. Descarga el ZIP. Si GitHub abre la ficha del archivo, pulsa **Download raw file**.
2. En **Archivos / Descargas**, extrae el ZIP.
3. Abre **consumo-sin-internet.html** con un navegador compatible con HTML local; elige Chrome si tu teléfono lo ofrece y ejecuta correctamente la aplicación.
4. Pulsa **Nueva captura** o importa un respaldo JSON/Excel.

No necesita instalación de servidor ni usuario/contraseña. El navegador debe ejecutar JavaScript y permitir almacenamiento local. Si Android solo muestra una vista previa, los botones podrían no funcionar; hay que abrir el archivo con un navegador compatible.

La descarga comienza vacía para no publicar tus capturas privadas. Los datos se guardan en ese dispositivo/navegador: usa los respaldos para conservarlos. Antes de cambiar de archivo o navegador, respalda el panel anterior.

Guía completa: [USO_SIN_INTERNET.md](USO_SIN_INTERNET.md).

## Integración final con Artron

Se reutilizarán **el login y los permisos existentes de Artron**, sin añadir usuarios propios del módulo. La conexión con el servidor de Artron está pendiente. Instrucciones para su equipo: [INTEGRACION_LOGIN_ARTRON.md](INTEGRACION_LOGIN_ARTRON.md).

El HTML personal sin conexión puede copiarse/modificarse; la protección de los datos oficiales se aplica en el servidor de Artron cuando se realice la integración.

## Alternativa anterior: servidor independiente

Se conserva [el paquete anterior con servidor y cuentas propias](entregas/consumo-artron-con-permisos.zip) y [su guía](INSTALACION_SERVIDOR.md) como referencia. **No se necesita para la prueba sin internet y no es el mecanismo de acceso elegido para Artron.**
