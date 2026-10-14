# Integración prevista con el login existente de Artron

Decisión actual: el módulo **no tendrá un inicio de sesión propio** en Artron. Artron controla quién puede entrar y qué operaciones permite a cada usuario mediante su sesión y permisos existentes. El HTML local entregado ahora no tiene usuarios y funciona sin conexión. La conexión con el servidor de Artron queda pendiente porque no se ha proporcionado su tecnología, API ni mecanismo de sesión.

## Trabajo del equipo de Artron

1. Añadir Consumo como módulo protegido por su sesión actual. Asignar el acceso a los usuarios o perfiles correspondientes.
2. Conectar lectura y guardado de capturas a una API de Artron y a su almacenamiento compartido. No usar `localStorage` como base oficial multiusuario.
3. Verificar la sesión y los permisos en **cada petición al servidor**, incluidas importaciones, correcciones y eliminaciones. No basta con ocultar el menú o un botón. La identidad y permisos deben proceder de la sesión verificada de Artron, no de un rol editable enviado por JavaScript.
4. Aplicar las validaciones de consumos, unidades normalizadas a GB, equipos/mes, serie e IMEI también en el servidor. Conservar pendientes sin sumarlos a los indicadores y prevenir que un guardado sobrescriba los cambios de otro usuario.
5. Registrar quién creó, corrigió o eliminó cada captura y la fecha del cambio. Ofrecer los permisos de captura, corrección/administración y consulta que defina Artron; no hace falta crear otro directorio de usuarios.
6. Migrar el respaldo local después de revisar la vista previa y conservar el original. No publicar las capturas como un JSON estático.

## Archivos útiles

- `src/main.js`: interfaz y flujo de captura/importación.
- `src/domain.js`: reglas de unidades, validación y agregaciones.
- `src/storage.js`: persistencia local del HTML personal.
- `src/access.js`: adaptador actual para el servidor independiente; se debe adaptar al contrato de sesión/API de Artron.
- `server/records.mjs`: referencia de validación del servidor, versiones y autorización de escrituras.

El paquete anterior `consumo-artron-con-permisos.zip` es una alternativa con servidor e identidad propios. **No es el archivo para probar sin red y no es el mecanismo de identidad elegido para la integración final.** Su servidor no confía automáticamente en la sesión de Artron: si se reutiliza, debe reemplazarse o conectarse su autenticación mediante una integración verificada por el equipo de Artron. No se debe dejar la API sin autenticación ni aceptar encabezados de identidad arbitrarios.

Para pruebas actuales, usar `consumo-sin-internet.html`. Para uso compartido final, desplegar el módulo y su API en Artron. El modo compartido necesita conexión a ese sistema; sincronización offline con conflictos no está implementada.
