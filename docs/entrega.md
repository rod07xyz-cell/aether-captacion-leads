# Qué recibe el cliente

La herramienta se instala **en las cuentas del cliente** y se le entrega funcionando. AetherLabsAI no aloja ni gestiona sus datos.

## Funcionando en sus cuentas

- [ ] Workflow «Captación de leads web» importado y activo en **su** n8n.
- [ ] Tabla `leads` creada en **su** n8n.
- [ ] Credencial SMTP con **su** cuenta de correo.
- [ ] Credencial Groq con **su** clave de API (paga el consumo directamente a Groq).
- [ ] Formulario integrado en **su** web, con su política de privacidad enlazada.
- [ ] Textos personalizados: nombre, negocio, servicios, criterios de puntuación y enlace de reservas.

## Documentación

- [ ] Manual de uso de una página: dónde ver los leads, cómo cambiar su estado y qué significa la puntuación.
- [ ] Lista de cuentas y credenciales creadas, con quién es el titular de cada una.
- [ ] Lista de proveedores que tratan datos (n8n o su alojamiento, el proveedor de correo y Groq) con el enlace a su acuerdo de tratamiento de datos (DPA), para que el cliente los acepte a su nombre.
- [ ] Texto para su política de privacidad: qué datos recoge el formulario, para qué, y que Groq solo recibe el sector y los servicios.

## Pruebas hechas con el cliente

- [ ] Envío con email y con teléfono.
- [ ] Envío marcando varios servicios.
- [ ] Antispam (campo oculto relleno) y contacto no válido.
- [ ] Recepción de los dos emails (aviso y confirmación) fuera de la carpeta de spam.

## Traspaso

- [ ] Accesos de desarrollo revocados al terminar.
- [ ] Sin copias de datos reales en equipos de AetherLabsAI (el desarrollo se hace con datos ficticios).

## Recurrente (opcional)

- **Mantenimiento**: ajustes de textos, servicios o criterios, cambios de modelo de IA cuando el proveedor retire uno y revisión de incidencias. Si incluye acceso a su n8n, se firma un contrato de encargado del tratamiento limitado al mantenimiento.
- **Consumo de IA**: lo paga el cliente a Groq con su propia clave (menos de una décima de céntimo por lead).
