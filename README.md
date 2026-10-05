# Simulador de Electrocardiografía con Tutor IA

Simulador educativo de ECG de 12 derivaciones,  con un tutor de inteligencia artificial que funciona sin internet. Está pensado para personas que no conocen el equipo, para estudiantes de áreas biomédicas y para técnicos de mantenimiento de electrocardiógrafos.

https://jlo8952.github.io/simulador-ecg/


---

## Características

- **ECG de 12 derivaciones** dibujado en papel milimetrado (25 mm/s, 10 mm/mV), con trazo en vivo y latido anotado (ondas P, QRS y T, intervalos PR y QT).
- **Medidas automáticas** de FC, P, PR, QRS y QTc, con colores según se acerquen o no a lo normal.
- **Controles de onda intuitivos:** 8 casos listos (normal, bradicardia, taquicardia, QRS ancho, T invertida, sin onda P, potasio alto, voltaje bajo) y 9 deslizadores con franja verde de valor normal. Un cuadro explica en lenguaje simple lo que ocurre con la señal.
- **Paciente simulado:** ficha con edad, peso, altura, presión y antecedentes que el tutor usa para personalizar sus respuestas.
- **Tutor IA local:** chat con una base de conocimiento propia (más de 180 términos) que entiende sinónimos y errores de ortografía. Es **ampliable** importando archivos JSON o desde la ventana de administración.
- **Dos redes neuronales propias**, escritas desde cero y entrenadas en el navegador: una clasifica el tipo de latido y otra interpreta las preguntas. Se visualizan en el *Laboratorio de IA*.
- **Alarma de paciente en peligro:** banner, luces parpadeantes y aviso por Telegram (alerta amarilla y alarma roja).
- **Sesión de aprendizaje:** registra el nombre del estudiante, el chat, los controles usados, los casos explorados y las capturas, y genera un **informe profesional** en HTML o PDF.
- **Integración con Telegram sin servidor:** el docente ve el chat en espejo, recibe capturas con los parámetros modificados, alarmas e informes, y puede controlar el simulador con comandos.


---

## Cómo usarlo

**Opción 1: en línea.** Abre la demo: https://jlo8952.github.io/simulador-ecg/

**Opción 2: sin internet.**
1. Descarga el archivo `index.html`.
2. Haz doble clic para abrirlo en Google Chrome o Microsoft Edge.
3. Escribe tu nombre y pulsa **Comenzar sesión**.

No requiere instalación ni dependencias. Lo que hace cada persona se guarda solo en su navegador.

---

## Guía rápida

| Quiero… | Hago esto |
|---|---|
| Ver un caso | En *Controles de onda*, pulso un caso (por ejemplo *QRS ancho*) |
| Ajustar la señal | Muevo un deslizador; ↺ lo devuelve a su valor normal |
| Preguntar algo | Escribo en el chat o pulso una pregunta sugerida |
| Congelar el trazo | Pulso **Pausar trazo** |
| Volver a lo normal | Pulso **Todo normal** |
| Terminar y obtener el informe | Pulso **Finalizar sesión** |
| Abrir la administración | Escribo `admin` en el chat |

### Alarma de paciente en peligro

| Nivel | Condiciones |
|---|---|
| **Alarma roja** | FC < 40 o > 150 · QRS > 150 ms · sin onda P con FC > 120 o QRS > 120 · T invertida con QRS > 120 · patrón de potasio alto · QTc > 500 ms |
| **Alerta amarilla** | FC < 50 o > 130 · QRS > 120 ms · sin onda P · T invertida o alta · QTc > 470 ms · crisis hipertensiva en la ficha |

> Son criterios **didácticos**, no un estándar clínico.

---

## Ampliar el conocimiento del tutor

Escribe `admin` en el chat para abrir la ventana de administración. Allí puedes buscar, editar, agregar o borrar términos, y **importar o exportar** la base en JSON. También puedes enseñar desde el chat:

```
aprende: término = significado
```

Formato del archivo JSON (cada clave es el término, con sinónimos separados por `|`):

```json
{
  "pr|intervalo pr": "Medida de tiempo desde el inicio de la onda P hasta el inicio del QRS...",
  "qrs ancho|bloqueo de rama": "Los ventrículos tardan más de 120 ms en activarse..."
}
```

Las respuestas pueden incluir `{nombre}`, `{bpm}`, `{peso}` y `{diag}`, que se reemplazan por los datos actuales del paciente simulado.


---

## Conexión con Telegram (opcional)

Se configura completamente desde *admin → pestaña Telegram*:

1. En Telegram, abre **@BotFather**, escribe `/newbot` y copia el **token**.
2. Pégalo en **Token del bot** y pulsa **Verificar bot**.
3. Pulsa **Vincular mi chat** y escribe `/start` a tu bot.
4. Envía un mensaje de prueba y, si quieres, activa el envío del informe al finalizar.

**Qué recibes:** chat en espejo (💻 estudiante / 🤖 tutor), capturas con los parámetros modificados, alarmas con la condición del paciente y el informe al terminar la sesión.

**Comandos:** `/ayuda` · `/estado` · `/captura` · `/casos` · `/caso bradicardia` · `/fc 120` · `/informe`

> La página debe permanecer abierta y visible para que Telegram funcione. El token se guarda solo en el navegador de cada equipo, nunca dentro del archivo. Solo se acepta el chat vinculado.

---

## 👥 Casos de uso


---

## Tecnología

- HTML, CSS y JavaScript puros, sin librerías externas.
- Señal ECG sintetizada por código; canvas con animación por `requestAnimationFrame`.
- Redes neuronales tipo MLP programadas desde cero (clasificador de latidos y comprensión de preguntas).
- Almacenamiento en `localStorage`.
- Integración con la API de bots de Telegram directamente desde el navegador.

---

## Límites

- Es una herramienta **educativa**: los casos son simulados y no sirven para diagnosticar a pacientes reales.
- Las redes neuronales se entrenaron con señales generadas por este simulador.
- Telegram requiere internet y la página abierta.
- Si se borran los datos del navegador, la sesión no se recupera: descarga el informe al terminar.

---

## 📄 Licencia y autoría

Proyecto desarrollado por **John F Correa** con fines educativos.
Agrega aquí tu licencia (por ejemplo MIT) y los datos de contacto o de la institución.
