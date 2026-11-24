# App Bambú — prototipo de turnos

Prototipo navegable de la app de turnos del **Centro Terapéutico Integral Bambú**, que forma parte de la Fundación SiMas (Lavalle, Mendoza). El Bambú atiende a niños, niñas y adolescentes con discapacidad. Este prototipo existe para que el presidente de la Fundación (Lic. Diego Dalmasso) lo revise antes de avanzar con la versión real.

Es la segunda app del proyecto. La primera es la **App Fundación SiMas** (novedades, proyectos y donaciones), que está en el repositorio [simas-apps](https://github.com/waltergonzalves/simas-apps). Las dos comparten backend y criterios de diseño.

## Ver el prototipo

https://waltergonzalves.github.io/bambu-turnos/

En la compu se ve dentro de un marco de teléfono, con una nota de presentación y el selector Vista familia / Vista del centro. En el celular ocupa la pantalla completa.

Del repositorio: es público, para poder publicarlo gratis con GitHub Pages. Por eso solo lleva datos de ejemplo y lo que el Bambú ya publicó en su afiche; nunca credenciales, claves de Mercado Pago ni datos reales de familias o pacientes.

---

## Qué es (y qué no es)

- **Prototipo navegable (también llamado interactivo o mockup funcional):** se ve y se usa como la app real, pero con datos de ejemplo y sin backend.
- **No es un wireframe:** un wireframe es un boceto sin diseño, y este prototipo ya tiene el diseño final.
- **No es un scaffold ni un boilerplate:** esos términos se refieren a la estructura de código vacía de un proyecto.

## Estado actual

- `index.html`: prototipo en un solo archivo (HTML, CSS y JS, sin dependencias salvo Google Fonts). En la compu se ve dentro de un marco de teléfono, con una nota de presentación y un selector **Vista familia / Vista del centro**. En el celular ocupa la pantalla completa.
- Se ve abriendo `index.html` en cualquier navegador, o publicándolo con GitHub Pages.
- **De ejemplo:** la familia (Laura, con Tomás y Sofía), los profesionales, los servicios, los horarios, el monto de la seña ($8.000) y los pacientes de la vista del centro.
- **Simulado:** los pagos con Mercado Pago, los mensajes por WhatsApp, los recordatorios y los cambios de turnos (se pierden al recargar la página).
- **Real, tomado del afiche oficial:** el concurso "Mi lugar favorito" (fotos hasta el 30 de noviembre) y el Facebook "Centro terapéutico bambu -lavalle".

---

## Pantallas

### Vista familia

| Pestaña | Contenido |
|---|---|
| Inicio | Saludo a la familia; próximo turno en grande (día, hora, servicio, paciente y profesional) con Confirmar, Reprogramar y Cancelar; aviso para confirmar antes de las 12 h del día anterior; accesos rápidos; concurso del Bambú |
| Mis turnos | Próximos e historial, con el estado de cada turno. Al tocar un turno se abre el detalle con sus acciones |
| Pedir (botón central) | Paciente, servicio (con su profesional), tira de 10 días hábiles y horarios. Los horarios ocupados aparecen tachados. Si el día está completo, ofrece lista de espera |
| Novedades | Concurso "Mi lugar favorito" con botón para enviar la foto, y avisos del centro |
| Familia | Adulta responsable, pacientes con su cobertura, aclaración sobre los datos que guarda la app y preferencias de avisos |

### Vista del centro (demo)

- Agenda del día con el estado de cada turno.
- Contadores: confirmados, sin confirmar, cancelados y en lista de espera.
- Lista de espera, con botón **Ofrecer** para darle el horario liberado a otra familia.
- Botón para enviar recordatorios a quienes no confirmaron.

### Estados de turno

| Estado | Significado |
|---|---|
| Agendado | Turno reservado, todavía no está en la ventana de confirmación |
| Confirmá tu asistencia | Faltan menos de 48 h y la familia tiene que confirmar |
| Confirmado | La familia confirmó |
| Asistió | Turno cumplido (historial) |
| Ausente con aviso | La familia avisó que no iba (historial) |
| Cancelado | Turno cancelado; el horario pasa a la lista de espera |

---

## Seña

**Decisión tomada:** todo turno nuevo se reserva con una seña por Mercado Pago, sin importar la cobertura del paciente.

- El botón **"Pagar seña con Mercado Pago"** aparece siempre al confirmar un turno nuevo.
- La seña se descuenta de la sesión.
- Si se cancela con 24 h de anticipación, se devuelve.
- Al reprogramar no se cobra de nuevo: la seña pagada pasa al nuevo turno.
- En la versión real, el turno se confirma solo cuando Mercado Pago avisa que el pago se acreditó. Para eso hay que usar link o checkout, no transferencia por alias.

> **Pendiente de revisión jurídica antes de la versión real:** ver "Consideraciones legales".

---

## Identidad visual

- **Logo:** vector redibujado a partir del logo oficial (caña de bambú que forma la "b", con el corazón naranja). Está en el código como `LOGO`.
- **Colores:** verde agua Bambú `#1f9e95` como color principal, naranja `#f0843a` para las acciones (pedir turno, pagar), verde caña `#8cc152` de apoyo.
- **Tipografía:** Nunito, redondeada como la del logo.
- **Mascota:** panda en vector, inspirado en el del afiche del concurso.
- Tiene modo claro y oscuro.

---

## Funcionamiento previsto (versión real)

1. **Confirmación obligatoria:** se abre 48 h antes del turno y vence a las 12 h del día anterior. Si la familia no confirma, el horario se ofrece a la lista de espera.
2. **Recordatorio** por notificación o WhatsApp el día anterior.
3. **Lista de espera:** cuando se libera un horario, se avisa a la primera familia anotada para ese servicio y franja.
4. **Registro de ausencias sin aviso**, para que el centro pueda hablar con la familia.
5. **Mensajes:** el botón "Escribir al centro" abre WhatsApp con el número del Bambú.
6. **Panel del centro:** agenda por profesional y por día, carga de disponibilidad, gestión de la lista de espera y exportación a planilla.

### Arquitectura

- App web instalable (PWA), igual que la de la Fundación.
- **Backend aparte**, por ejemplo Supabase o Firebase, para el inicio de sesión de las familias, los turnos, la lista de espera y los avisos de pago de Mercado Pago.
- La clave privada de Mercado Pago y los datos reales **nunca** van al repositorio.

---

## Consideraciones legales

> Puntos a revisar antes de pasar a producción. No reemplazan el asesoramiento profesional de cada caso.

**Seña y cobertura de discapacidad (Ley 24.901, art. 2).** Las obras sociales deben dar cobertura total de las prestaciones básicas que necesiten sus afiliados con discapacidad, y quienes no tienen obra social acceden a ellas por medio del Estado. Si una prestación del Bambú se factura a una obra social (OSEP, prepagas) o a Incluir Salud, cobrarle una seña a la familia es objetable: puede generar reclamos de las familias o problemas con el financiador. Antes de la versión real hay que definir con Diego si la seña se mantiene para todos los pacientes o solo para los particulares. Si se cobra seña, conviene dejar por escrito su carácter: el art. 1059 CCyC la interpreta como confirmatoria salvo pacto en contrario. También hay que fijar la política de devolución.

**Datos de salud (Ley 25.326).** Los turnos de chicos con discapacidad son datos de salud, que la ley considera sensibles. La app guarda solo nombre, cobertura, turno, profesional y adulto responsable; nunca diagnósticos ni el certificado de discapacidad (CUD). Además hacen falta consentimiento informado, política de privacidad, inscripción de la base de datos ante la Agencia de Acceso a la Información Pública y medidas de seguridad acordes.

**Imagen de niños, niñas y adolescentes (Ley 26.061, art. 22).** El concurso de fotos y cualquier publicación con imágenes de chicos requieren el consentimiento de sus representantes. En la app conviene sumar un aviso de consentimiento al enviar la foto.

**Defensa del consumidor.** Si la relación con familias particulares es de consumo, las condiciones de la seña y de su devolución tienen que estar informadas de forma clara antes del pago.

---

## Datos pendientes

**Del Bambú:**
- Servicios que se dan con turno, profesionales y días u horarios de cada uno.
- Duración de las sesiones.
- Monto de la seña y política de devolución.
- Cómo se financian las prestaciones: obras sociales, Incluir Salud, particulares o una mezcla.
- Celular o WhatsApp del centro, y link al Facebook.
- Quién va a administrar la agenda en el panel.

**De la Fundación:**
- Cuenta de Mercado Pago para recibir las señas: ¿la de la Fundación o una propia del Bambú?
- Revisión de Diego sobre la seña (ver "Consideraciones legales").

---

## Hoja de ruta

- [x] Prototipo navegable con logo y colores del Bambú
- [x] Seña por Mercado Pago en todos los turnos nuevos (prototipo)
- [ ] Revisión de Diego
- [ ] Definición jurídica de la seña
- [ ] Inicio de sesión para familias (DNI o celular con código)
- [ ] Turnos y disponibilidad reales en el backend
- [ ] Mercado Pago real con confirmación automática del pago
- [ ] Recordatorios y confirmación obligatoria
- [ ] Lista de espera con avisos
- [ ] Panel del centro
- [ ] Publicación como PWA y, si hace falta, en Play Store

---

## Estructura del repositorio

```
bambu-turnos/
├── README.md
└── index.html      # Prototipo navegable (un solo archivo)
```

La App Fundación SiMas, el logo compartido y los documentos de consideraciones legales y decisiones están en [simas-apps](https://github.com/waltergonzalves/simas-apps).

---

## Fuentes

- Centro Terapéutico Integral Bambú. (2026). *¡Concurso! Mi lugar favorito* [Afiche].
- Fundación SIMAS. (2026). *Sitio institucional*. https://www.fundacionsimas.org.ar/
- Ley 24.901. (1997). *Sistema de Prestaciones Básicas en Habilitación y Rehabilitación Integral a favor de las Personas con Discapacidad*. https://www.argentina.gob.ar/normativa/nacional/47677/texto
- Ley 25.326. (2000). *Protección de los Datos Personales*.
- Ley 26.061. (2005). *Protección Integral de los Derechos de las Niñas, Niños y Adolescentes*.
- Ley 26.994. (2014). *Código Civil y Comercial de la Nación*.
- Mercado Pago. (2026). *Documentación para desarrolladores*. https://www.mercadopago.com.ar/developers/es/docs
