# Entrega Final — Ecosistema de Automatización IA Autónomo para Negocios

**Estudiante:** German Velasquez  
**Curso:** AI Automation — Coderhouse  
**Proyecto:** Ecosistema de generación de contenido con IA, RAG, resiliencia y control humano (HITL)  
**Empresa:** Grupo Estrategia y Marca LLC (GEYM)

---

## 1. Descripción del proyecto

Este proyecto implementa un ecosistema de automatización con inteligencia artificial para transformar una Idea Semilla registrada en Airtable en una pieza de contenido generada con IA y conocimiento contextual de la empresa.

El sistema incorpora RAG, control de estados, manejo de errores, trazabilidad y aprobación humana antes de ejecutar la acción final.

### Flujo implementado

**Airtable (Nueva) → RAG → OpenAI → Airtable (En Revisión) → Gmail de solicitud de aprobación → aprobación humana → HITL → Airtable (Publicado) → Gmail final**

---

## 2. Stack tecnológico

- **Make** — orquestación de los escenarios.
- **Airtable** — Centro de Comando, estados, trazabilidad y conocimiento.
- **OpenAI GPT-4o-mini** — generación de contenido.
- **RAG** — recuperación de conocimiento de Grupo Estrategia y Marca.
- **Gmail** — notificaciones de aprobación y salida final.

---

## 3. Escenario 1 — Generación IA + RAG + Resiliencia

El primer escenario:

1. Detecta nuevos registros en Airtable.
2. Procesa únicamente registros con Estado `Nueva`.
3. Consulta la base de conocimiento GEYM.
4. Agrega el contexto RAG.
5. Envía Idea Semilla + contexto a OpenAI.
6. Genera el borrador utilizando GPT-4o-mini.
7. Actualiza Airtable a `En Revisión`.
8. Envía por Gmail la solicitud de aprobación humana.

El modelo está configurado con un máximo de **400 tokens de salida**.

También incorpora un **Error Handler** que registra en Airtable:

- Resultado de ejecución.
- Estado de error.
- Tipo de error.
- Mensaje del error.
- Fecha de ejecución.

Se realizó una prueba controlada de error utilizando un modelo inexistente para provocar una respuesta `404` y validar la ruta de resiliencia.

---

## 4. Human-in-the-loop (HITL)

La publicación requiere intervención humana.

Después de generar el contenido, el sistema envía un correo indicando que existe una pieza pendiente de aprobación.

La persona responsable revisa el contenido en Airtable y marca el campo booleano:

`Aprobado = true`

El segundo escenario únicamente continúa cuando se cumplen simultáneamente:

`Aprobado = true`

y

`Estado = En Revisión`

Una vez aprobada la pieza:

**Airtable → Estado Publicado → Gmail final**

De esta manera ninguna pieza pasa a la acción crítica sin aprobación humana.

---

## 5. RAG — Base de conocimiento

El sistema utiliza una base de conocimiento de Grupo Estrategia y Marca con información atómica relacionada con:

- propuesta de valor;
- experiencia;
- metodología MENTUM;
- neuroventas;
- estrategia;
- tecnología y automatización;
- PNL;
- metodología de trabajo;
- tono de comunicación;
- contacto y CTA.

Make consulta operativamente la base:

**Conocimiento GEYM / Base de Conocimiento**

La tabla **Fuentes RAG** del Centro de Comando se utiliza como capa relacional y de trazabilidad.

---

## 6. Estados operativos

El sistema utiliza los siguientes estados:

- `Nueva`
- `En Revisión`
- `Publicado`
- `Error`

Esto permite controlar el ciclo de vida de cada pieza y evitar reprocesamientos.

---

## 7. Dashboard

Se desarrolló un dashboard en Airtable para visualizar:

- Total de piezas.
- Publicadas.
- En Revisión.
- Errores.
- Tasa de Error.

Las evidencias incluidas en la documentación corresponden al snapshot tomado durante la validación del proyecto.

---

## 8. Pruebas realizadas

El ecosistema fue sometido a múltiples ejecuciones, incluyendo:

- generación exitosa;
- recuperación RAG;
- actualización de Airtable;
- solicitud de aprobación;
- bloqueo antes de aprobación;
- aprobación humana;
- publicación;
- Gmail final;
- prueba controlada de error 404.

Se realizaron al menos **5 ejecuciones**, incluyendo happy path y unhappy path.

---

## 9. Documentación

Este repositorio contiene:

### Documento maestro

`Entrega_Final_Coderhouse_AI_Automation_German_Velasquez.pdf`

Incluye arquitectura, modelo de datos, RAG, costos, resiliencia, HITL, dashboard, seguridad, evidencias y matriz de cumplimiento.

### Documentos técnicos

- `01_Arquitectura_con_Evidencias_German_Velasquez_ACTUALIZADO.docx`
- `02_Manual_Datos_JSON_con_Evidencias_German_Velasquez_ACTUALIZADO.docx`
- `03_Matriz_Costos_con_Evidencias_German_Velasquez_ACTUALIZADO.docx`
- `04_Seguridad_Resiliencia_HITL_con_Evidencias_German_Velasquez_ACTUALIZADO.docx`
- `05_Dashboard_KPIs_con_Evidencias_German_Velasquez_ACTUALIZADO.docx`

---

## 10. Blueprints Make

Se incluyen los dos Blueprints finales exportados desde Make:

### Escenario 1
**Generación IA + RAG + Resiliencia**

Incluye generación, RAG, OpenAI, actualización de Airtable, Error Handler y solicitud de aprobación por Gmail.

### Escenario 2
**Publicación Aprobada — HITL**

Incluye Watch Records, validación de aprobación, actualización a Publicado y Gmail final.

---

## 11. Seguridad

Para la entrega:

- No se publican API Keys.
- No se publican tokens.
- Las credenciales permanecen protegidas dentro de las conexiones de Make.
- Los datos operativos se manejan mediante variables dinámicas.
- La acción crítica requiere aprobación humana.
- Los errores quedan registrados para auditoría.

---

## 12. Evidencias

La documentación contiene capturas reales de:

- escenarios de Make;
- Airtable;
- base RAG;
- Error Handler;
- solicitud de aprobación;
- ejecución HITL;
- Gmail recibido;
- dashboard;
- pruebas exitosas y de error.

Estas evidencias documentan la ejecución real del ecosistema y no solamente su diseño conceptual.

---

## 13. Video demostrativo

El video de demostración de máximo 3 minutos presenta el funcionamiento completo del ecosistema y evita mostrar credenciales, tokens o secretos.

**Enlace al video:** PENDIENTE DE INCORPORAR

---

## Autor

**German Velasquez**  
Grupo Estrategia y Marca LLC  
AI Automation — Coderhouse
