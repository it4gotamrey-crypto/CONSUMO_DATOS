# Consumo para Artron · usuarios y permisos · v1.6

Esta entrega incorpora un servidor real y una base SQLite compartida. Los permisos se aplican en la API, incluso si alguien cambia el HTML o envía solicitudes manualmente. Está preparada y probada en el entorno de desarrollo; todavía no está instalada en el servidor de Artron.

El HTML local anterior sigue siendo una herramienta personal: no protege datos oficiales ni admite permisos fiables sin servidor. En la versión con acceso controlado se consulta y captura mediante la dirección de Artron. Para guardar cambios necesita conexión con ese servidor.

## Permisos

| Acción | Administrador | Capturista | Consulta |
|---|---|---|---|
| Consultar datos, históricos, filtros e imprimir | Sí | Sí | Sí |
| Personalizar las gráficas de su navegador | Sí | Sí | Sí |
| Crear nuevas capturas validadas | Sí | Sí | No |
| Corregir o eliminar capturas existentes | Sí | No | No |
| Confirmar consumos atípicos | Sí | No | No |
| Importar Excel o restaurar JSON, incluidos pendientes | Sí | No | No |
| Administrar accesos y consultar el registro de cambios | Sí | No | No |
| Respaldar JSON y exportar CSV/Excel desde el panel | Sí | No | No |

Capturista puede crear capturas de los equipos del módulo. No se ha definido una restricción por departamento o usuario asignado. Consulta puede leer los datos mostrados en el panel; el permiso de lectura permite conservar una copia de la información que ya puede ver. El código que ejecuta un navegador también es visible. La protección consiste en impedir cambios no autorizados en el servidor.

## Instalar y crear el primer administrador

Requisitos: **Node.js 24**, npm y un disco persistente para SQLite. El módulo no usa servicios de identidad externos ni contraseñas predeterminadas. Por ahora tiene usuarios propios, porque no se ha proporcionado el mecanismo de acceso de Artron.

Desde la carpeta del proyecto o del paquete:

```bash
npm ci
npm run build
npm run admin:create -- administrador "Nombre del administrador"
npm start
```

El comando de alta pide dos veces una contraseña de al menos 12 caracteres y no la muestra en pantalla. No la escribas dentro del HTML, en el código fuente ni en la línea del comando. En el paquete de servidor ya construido, `dist/` está listo y no hace falta construirlo otra vez. El servidor usa solo módulos incluidos en Node.js.

Abre el servicio desde la dirección configurada, inicia sesión y entra a **Usuarios y permisos** para dar de alta Capturistas y usuarios de Consulta. Puedes cambiar permisos, desactivar cuentas y restablecer contraseñas. Esos cambios revocan las sesiones del usuario. No se permite dejar el módulo sin un administrador activo. Usa otro administrador para cambiar tu propio rol o desactivar tu cuenta.

## Montar dentro de Artron

El equipo de Artron debe ejecutar el servicio como proceso administrado, detrás de su proxy HTTPS. Ejemplo de configuración de entorno, sin contraseñas:

```dotenv
NODE_ENV=production
HOST=127.0.0.1
PORT=8080
CONSUMO_ORIGIN=https://DOMINIO-REAL-DE-ARTRON
CONSUMO_BASE_PATH=/modulos/consumo
CONSUMO_DB=/RUTA-PRIVADA-PERSISTENTE/consumo.sqlite
```

Sustituir dominio y ruta por los reales. Usar el mismo `CONSUMO_DB` al crear al administrador y al iniciar el servicio. No colocar la base en una carpeta pública. El proxy debe reenviar `/modulos/consumo/` al puerto interno **conservando ese prefijo**. El servicio solo acepta solicitudes de escritura cuyo origen coincida con `CONSUMO_ORIGIN`.

Ejemplo orientativo para Nginx dentro del sitio HTTPS de Artron:

```nginx
location /modulos/consumo/ {
    proxy_pass http://127.0.0.1:8080;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-Proto https;
    client_max_body_size 10m;
}
```

Alojar la pantalla y su API en el mismo origen. Agregar al menú de Artron un enlace a `/modulos/consumo/`, o mostrar esa ruta en un iframe del mismo origen. Si se usa iframe con sandbox, permitir scripts, same-origin, modals y downloads para impresión/exportación autorizada. El encabezado de seguridad permite marcos del mismo origen.

Servir el módulo mediante este proceso, no únicamente como archivos estáticos. El servidor entrega la marca de modo protegido en la página; los archivos HTML abiertos por su cuenta no son el módulo con permisos.

Si Artron ya tiene inicio de sesión, su equipo puede sustituir la autenticación propia por un adaptador de su identidad verificada. Debe mantener la autorización de cada operación en el servidor. No confiar en un rol enviado desde JavaScript, un parámetro URL o un encabezado externo sin verificación. No se ha conectado ni publicado nada en Artron desde este entorno.

## Pasar las capturas actuales al servidor

El servidor comienza vacío; no importa automáticamente datos privados del HTML, `localStorage` o archivos de referencia. Así no sustituye capturas más recientes.

1. En el panel local que ya usas, abre **Respaldar y exportar → Respaldo completo JSON**.
2. En el módulo del servidor, inicia sesión como Administrador.
3. Entra a **Respaldo y exportación → Restaurar un respaldo**, elige el JSON y revisa la importación antes de confirmar.
4. Verifica período, unidades y registros pendientes. Corrige con las lecturas reales.

La compatibilidad con las 41 capturas originales de JULIO fue verificada. Sus 11 pendientes no se convierten en consumo válido por trasladarlas. Un total validado parcial sigue siendo parcial. Los duplicados por equipo/mes se rechazan, incluso intercambiando IMEI 1 e IMEI 2. Conserva siempre el respaldo previo.

El servidor vuelve a validar lecturas, meses, aplicaciones, sumas, series/IMEI y confirmaciones de valores atípicos. Solo Administrador puede importar registros pendientes; se conservan y quedan excluidos de los indicadores. Los guardados tienen una versión: si otro usuario cambia los datos, el panel los actualiza y solicita revisar antes de volver a guardar.

## Sesiones, auditoría y respaldos

Las contraseñas se guardan con scrypt y sal aleatoria. Las sesiones usan tokens aleatorios cuyo hash se persiste en SQLite, cookies HttpOnly/SameSite=Strict y Secure en HTTPS. Caducan a las 8 horas; salir revoca la sesión. Las escrituras requieren un token CSRF y origen autorizado. Hay límites de tamaño, tiempo e intentos de acceso.

Los cambios de capturas registran usuario, fecha y valores anteriores/nuevos; las altas y cambios de cuentas también se registran, sin incluir contraseñas. **Registro de cambios** muestra los últimos 200 eventos al administrador. La base conserva el historial completo. Los administradores del sistema operativo y la base de datos tienen acceso técnico a esos archivos; este registro no es un sistema externo de auditoría inmutable.

Para respaldo de toda la instalación, detener el proceso y copiar `consumo.sqlite`; iniciar de nuevo al terminar. No copiar únicamente el archivo principal mientras el proceso está activo: SQLite usa WAL. Para un respaldo activo, el equipo puede usar la herramienta oficial de backup de SQLite. El JSON del panel respalda capturas, pero no usuarios ni auditoría. Mantener una sola instancia del servicio con un disco local persistente; no colocar la base en un recurso de red compartido.

## Verificación

```bash
npm test
npm run build
npm run test:access-browser
```

Las pruebas verifican intentos directos de saltarse permisos, rol falsificado, validaciones del servidor, conflictos entre sesiones, cookies, origen/CSRF, caducidad y revocación de sesiones, alta/baja de usuarios, auditoría y captura/impresión en navegador. Usan usuarios, contraseñas y consumos ficticios en bases temporales que se eliminan al terminar.
