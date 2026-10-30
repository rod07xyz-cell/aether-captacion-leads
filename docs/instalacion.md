# Instalación paso a paso

Probado con n8n 2.x (nodos de Data Tables, LangChain y Groq). Tiempo aproximado: 30 minutos.

## 1. Tabla `leads`

En n8n → **Data Tables** → *Create*, crea una tabla llamada `leads` con estas columnas:

| Columna | Tipo | Contenido |
|---|---|---|
| `nombre` | string | Nombre del contacto |
| `email` | string | Email (si dejó email) |
| `telefono` | string | Teléfono (si dejó teléfono) |
| `empresa` | string | Nombre del negocio |
| `tipo_negocio` | string | Sector elegido |
| `servicios` | string | Servicios marcados, separados por `; ` |
| `mensaje` | string | Mensaje libre (solo formularios antiguos) |
| `puntuacion` | number | 1-100; `0` = sin evaluar |
| `motivo_puntuacion` | string | Explicación de la IA |
| `origen` | string | Siempre `Web` |
| `estado` | string | `Nuevo` al entrar; cámbialo a mano (`Contactado`, `Cliente`…) |
| `proxima_accion` | string | `Responder en menos de 24 h` |
| `fecha_proxima_accion` | date | Fecha límite para responder |
| `recibido` | date | Fecha de entrada |

Copia el **ID de la tabla** (aparece en la URL al abrirla).

## 2. Credenciales

En n8n → **Credentials** → *Add credential*:

- **SMTP**: servidor, puerto, usuario y contraseña de la cuenta que enviará los emails (la de tu dominio).
- **Groq**: tu clave de API de [console.groq.com/keys](https://console.groq.com/keys). Mejor una clave solo para este workflow, para poder revocarla sin afectar a nada más.

## 3. Importar el workflow

1. *Workflows → Import from file* → `workflows/captacion-leads.json`.
2. Abre cada nodo marcado en rojo y asigna la credencial: **Groq (evaluación)** y **Groq (frase)** → Groq; **Avisarme por email** y **Confirmar al contacto** → SMTP.
3. En **Guardar en tabla leads**, elige tu tabla `leads` (sustituye `CONFIGURAR_ID_TABLA_LEADS`).

## 4. Personalizar

| Dónde | Qué cambiar |
|---|---|
| **Formulario web** → *Allowed Origins* | Tus dominios (`https://tu-dominio.es,https://www.tu-dominio.es`) |
| **Evaluar con IA** → mensaje de sistema | `[TU NOMBRE] ([TU NEGOCIO])`, qué ofreces y tu cliente ideal; ajusta los criterios de puntuación a tu negocio |
| **Personalizar con IA** → mensaje de sistema | `[TU NOMBRE]` y los servicios que ofreces |
| **Avisarme por email** | Remitente y destinatario (`hola@tu-dominio.es`) |
| **Confirmar al contacto** | Remitente, `[TU NOMBRE]`, `[TU NEGOCIO]`, enlace de reservas (`cal.eu/tu-usuario/30min`) y enlace a tu política de privacidad |
| **Normalizar lead** | Las listas de sectores y servicios **si cambias los del formulario** (deben coincidir exactamente) |
| **Groq (…)** | El modelo, si `openai/gpt-oss-120b` deja de estar disponible (lista actual en la consola de Groq) |

Busca `[TU`, `tu-dominio.es`, `tu-usuario` y `CONFIGURAR` para no dejarte nada.

## 5. Formulario

1. Activa el workflow (*Publish*) y copia la **URL de producción** del nodo *Formulario web* (termina en `/webhook/lead-web`).
2. En `formulario/index.html`, cambia `WEBHOOK_URL` y `EMAIL_RESPALDO`, y el enlace a tu política de privacidad.
3. Integra el formulario en tu web o publícalo tal cual. Debe servirse desde uno de los dominios de *Allowed Origins*: desde `localhost` o `file://` el envío fallará por CORS (es lo esperado).

## 6. Probar

1. Envía el formulario con tu email y varios servicios marcados.
2. En n8n → *Executions*, comprueba que todos los nodos están en verde, la puntuación en **Guardar en tabla leads** y la frase en **Personalizar con IA**.
3. Revisa los dos emails (el aviso y la confirmación). Si no llegan, mira la carpeta de spam y los registros SPF y DKIM de tu dominio.
4. Prueba el antispam: rellena a mano el campo oculto `website` y comprueba que la ejecución se detiene en **Descartar spam y vacíos**.
