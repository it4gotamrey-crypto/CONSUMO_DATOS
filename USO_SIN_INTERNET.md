# Usar Consumo sin internet y sin usuarios propios

Esta es la versión local para empezar a probar. Es un único archivo **consumo-sin-internet.html** con el programa, estilos y gráficas incorporados. No pide usuario, contraseña ni conexión a un servidor. La conexión solo es necesaria para descargarlo inicialmente.

## Abrirlo

1. Descarga `consumo-sin-internet.zip` desde GitHub.
2. Abre **Archivos / Descargas** en tu celular o computadora y extrae el ZIP.
3. Abre **consumo-sin-internet.html** con un navegador que ejecute HTML local y permita almacenar datos.
4. Pulsa **Nueva captura**. Conserva siempre las unidades MB o GB: `825 MB` equivale a `0.825 GB`.

No hace falta instalar Node.js, ejecutar comandos ni instalar un servidor. El archivo no es una aplicación Android o iOS y no se instala desde una tienda. Algunos gestores de archivos de Android/iPhone muestran únicamente una vista previa, y algunos navegadores restringen los archivos HTML locales o su almacenamiento. Si los botones no responden o el panel avisa de un problema de almacenamiento, no captures datos allí; prueba un navegador compatible o la versión de computadora. Esta entrega no afirma compatibilidad con todos los navegadores de celular.

## Capturas

La descarga de GitHub comienza vacía: no publica las capturas privadas de JULIO. Para trasladar los datos del panel anterior, exporta un **Respaldo completo JSON** desde esa copia y restáuralo en **Respaldo y exportación → Restaurar un respaldo** del archivo nuevo. Revisa la vista previa antes de confirmar. También puedes importar tu Excel seleccionando la hoja correcta y sus unidades.

Las capturas se guardan en el navegador y dispositivo que uses. No se comparten automáticamente con otros celulares. Exporta respaldos periódicos: borrar los datos del navegador o cambiar de aplicación/ruta del archivo puede dejarte sin acceso a esa copia local. No elimines el panel anterior hasta comprobar tu respaldo y la restauración.

Puedes capturar, revisar, ver los históricos, elegir una o varias gráficas, ajustar su tamaño y preparar la impresión sin conexión. La impresión física depende del servicio de impresión del celular y de cómo se conecte a la impresora; generar el reporte no necesita el servidor de Artron.

## Interfaz sin exportación del código

La versión **1.6.1** elimina las opciones **Guardar panel**, **Copiar HTML** y **Descargar panel**. Se conservan importación de Excel, respaldos JSON, descarga del reporte en Excel/CSV e impresión. Esto retira la función de copiar el programa desde su interfaz; un archivo HTML local sigue siendo un archivo que su propietario puede copiar o modificar.

## Descargar Excel (.xlsx)

En **Respaldar y exportar**, pulsa **Descargar Excel**. También está disponible en **Capturas mensuales**. Genera un archivo `.xlsx` real sin conexión, con ocho pestañas: Resumen, Capturas, Detalle apps, Por aplicación, Por usuario, Por departamento, Por período y Estado equipos.

Respeta los filtros de período, departamento y búsqueda. Los pendientes quedan identificados en el detalle y fuera de los totales validados. Los IMEI, números de empleado y series conservan sus ceros iniciales. Las celdas sin lectura quedan vacías; los ceros son lecturas de cero. Los resúmenes son tablas de datos; las gráficas del panel se imprimen con **Imprimir reporte**.

Excel es el reporte para consultar y trabajar con los datos. Para trasladar todas tus capturas al actualizar el HTML o restaurar el panel, conserva el **respaldo JSON**. Antes de sustituir tu archivo anterior, expórtalo y comprueba su restauración en el nuevo archivo.

## Cuando se integre a Artron

La decisión actual es **reutilizar el login y los permisos que Artron ya tiene**, sin agregar cuentas o contraseñas propias a este módulo. Ver [INTEGRACION_LOGIN_ARTRON.md](INTEGRACION_LOGIN_ARTRON.md).

Por ahora, quien tenga el HTML puede modificar su copia local. La protección de los datos oficiales se aplicará en el servidor de Artron. Abrir un HTML sin conexión no ofrece una autoridad central que impida a su dueño modificar esa copia.
