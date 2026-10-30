# Privacidad desde el diseño

Notas técnicas de cómo trata los datos el workflow. **No son asesoramiento jurídico**: cada negocio debe revisar su política de privacidad y su registro de actividades con su asesor.

## Qué datos se recogen

Nombre, negocio, sector, email o teléfono y servicios de interés. Nada de datos de salud ni texto libre en el formulario actual.

## Qué sale hacia la IA (Groq)

| Dato | ¿Sale a Groq? |
|---|---|
| Sector | Sí, solo si es uno de los valores del formulario (si no, «Otro») |
| Servicios marcados | Sí, solo los valores exactos del formulario |
| Si el contacto es email o teléfono | Sí, sin el contacto en sí |
| Nombre, negocio, email, teléfono | **No** |
| Mensaje libre (formularios antiguos) | Solo tras sustituir emails, teléfonos y enlaces por `[email]`, `[teléfono]` y `[enlace]` |

Groq está en EE. UU.: el responsable debe comprobar la garantía de la transferencia (Marco de Privacidad de Datos UE-EE. UU. o cláusulas contractuales tipo) e informar en su política de privacidad.

## Protecciones

- **Lista blanca** de sector y servicios: no se pueden colar instrucciones a la IA desde el formulario.
- **Revisión de la respuesta de la IA** antes de enviarla al contacto (sin enlaces, emails, HTML ni cifras; longitud y final controlados); si no la pasa, se usa la plantilla fija.
- **Limpieza del nombre** antes de insertarlo en el email.
- **Antispam** con campo trampa y validación del contacto.
- **CORS** limitado a los dominios del negocio.
- **Sin decisiones automatizadas con efectos**: la puntuación solo ordena las respuestas; todas las solicitudes se atienden (art. 22 RGPD).

## Conservación

La tabla `leads` no borra nada sola. Define un plazo (por ejemplo, 12 meses si no hay colaboración) y bórralos a mano o con un workflow programado.
