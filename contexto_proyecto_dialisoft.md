# Contexto del proyecto Dialisoft

> **Documento de contexto para una prueba de lectura con ChatGPT**  
> Fecha de elaboración: 17 de noviembre de 2026  
> Estado: **resumen de contexto y propuesta en evaluación; no constituye un procedimiento aprobado**.

## 1. Propósito de este archivo

Este archivo reúne la información compartida en las conversaciones sobre la **propuesta para optimizar el proceso general de levantamiento, análisis, diseño y documentación de requerimientos de Dialisoft**. Puede utilizarse como contexto inicial para un asistente de inteligencia artificial (IA) que apoye a los analistas.

**Alcance del conocimiento:** el resumen se basa en lo expresado en la conversación y en secciones consultadas de los documentos de ejemplo y manuales disponibles. **No es un inventario completo de todos los módulos, procesos, tablas o estándares de Dialisoft.** Debe distinguirse lo observado en las fuentes, lo confirmado por el usuario y las propuestas pendientes de aprobación.

## 2. Contexto general y forma de trabajo actual

- Dialisoft cuenta con módulos y funcionalidades cuya evolución requiere documentación funcional y técnica detallada.
- En el proceso descrito, **el analista se reúne con el cliente para entender la necesidad** y después construye el requerimiento; también **consulta requerimientos anteriores, copia estructuras y las adapta**. El usuario identificó esta combinación como **A + C**.
- El analista tiene responsabilidad sobre el análisis funcional **y sobre una parte muy amplia del diseño técnico**: tablas, campos, relaciones, validaciones, comportamiento de botones, consultas, procesos e integraciones. No se confirmó un rol separado y permanente de arquitectura técnica.
- El trabajo no consiste solo en redactar historias de usuario: en ocasiones entrega instrucciones de implementación con suficiente precisión para desarrollo.
- En respuesta a la pregunta de dónde se invierte más tiempo, el usuario ordenó las opciones **C → D → E → B**: **C**, redactar el documento y describir botones, campos, validaciones e imágenes; **D**, corregirlo cuando aparecen condiciones nuevas; **E**, el conjunto de actividades del proceso; **B**, investigar cómo funcionan los módulos, tablas y consultas existentes. La opción E era una categoría general y no una tarea independiente.

### Problemas y oportunidades identificados

1. **Redacción repetitiva:** se vuelve a describir el comportamiento de componentes similares ya utilizados en otros módulos.
2. **Reprocesos:** las condiciones y excepciones descubiertas tarde obligan a modificar secciones de requerimientos extensos.
3. **Búsqueda manual de antecedentes:** los analistas consultan grandes PDF históricos, seleccionan partes y las adaptan.
4. **Concentración de información:** interfaces, base de datos, lógica, integraciones y pruebas aparecen dentro de documentos extensos difíciles de mantener.
5. **Trazabilidad mejorable:** conviene poder relacionar cada funcionalidad con sus reglas, decisiones, estructuras y pruebas.

**Objetivo de la propuesta:** reducir el tiempo de elaboración y las correcciones, aumentar la reutilización de conocimiento y conservar la precisión funcional y técnica. **No se busca reducir páginas a costa de eliminar información necesaria.**

## 3. Fuentes conocidas del proyecto

### 3.1 Requerimiento usado como ejemplo

Documento proporcionado: **`RQ0002024 - Implementar consulta, importación y reporte de glosas SIIFA en Glosas y Devoluciones.pdf`**, de **241 páginas**. En su contenido aparece también un número de requerimiento diferente en la primera página (**0002030**); conviene verificar la versión y el identificador oficial antes de publicarlo en un catálogo.

En las secciones consultadas se describen, entre otros temas:

- Integración del módulo Glosas y Devoluciones con **SIIFA** y **GlosasII**.
- Consulta, sincronización, distribución e importación de glosas y devoluciones.
- Importación de reiteraciones, respuestas, historial de glosas/devoluciones/pagos y reportes en Excel.
- Estructuras de base de datos, reglas de identificación y asociación, validaciones antes de importar, botones, alertas, controles de permisos y pruebas de comportamiento implícitas en los requisitos.

**Ejemplo de regla de negocio delicada (página 8):** una factura puede tener varios seguimientos SIIFA independientes; no deben fusionarse por compartir factura o código. Varias glosas SIIFA de una misma factura pueden originar **una sola cabecera local** en `public.glosas`, pero los seguimientos y los detalles asociados deben conservar su identidad para respuestas y reiteraciones. Esto ilustra por qué la estandarización **no debe borrar excepciones ni reglas específicas**.

**Ejemplo de validación relevante (páginas 89–90):** antes de importar cada factura se vuelven a comprobar su existencia, sede y condiciones de disponibilidad. Una acción masiva no elimina la necesidad de validar individualmente las facturas.

**Ejemplo de desacoplamiento de permisos (páginas 235–236):** la disponibilidad del reporte Excel no debe depender de la variable que habilita la importación; el permiso de reporte y la existencia de facturas seleccionadas son controles separados.

### 3.2 Manuales de programación disponibles

- **`Manual Programación Reingeniería 4.0 SQL.pdf`**: contempla convenciones SQL como uso de esquemas, alias/abreviaciones, validación de estados, trazabilidad e indicaciones de rendimiento; el texto del manual propone como referencia un tiempo máximo de consulta de **300 ms**. No se debe asumir cumplimiento sin medición.
- **`Manual Programación Reingeniería 4.0 PHP.pdf`**: documenta estructura de vistas, controladores, modelos, organización del código, responsabilidades de archivos y control de acceso/token. Entre los ejemplos consultados: `view/`, `view/modal/`, `assets/js/`, `assets/css/` y controladores asociados a vistas.
- **`Manual Programación Reingeniería 4.0 JS.pdf`**: documenta estructura de variables y funciones, archivos de peticiones, funciones asíncronas y documentación de parámetros. Entre los ejemplos consultados: `assets/js/`, `nombre_modulo_peticiones.js`, uso de `petición_fetch` y `validar_estado_peticion_ajax`.
- También se suministraron archivos **`Abreviaciones DESARROLLO DIALISOFT.xlsx`** y **`Abreviaciones DIALISOFT.xlsx`** como referencias de nomenclatura. **Su contenido detallado no se reproduce aquí ni se declara validado en este resumen**.

Los manuales deben tratarse como **fuentes técnicas a consultar**, no como sustitutos de las reglas particulares de cada requerimiento.

## 4. Preparación propuesta antes de aplicar las cinco etapas

Estas son **iniciativas propuestas**, todavía no declaradas como implementadas o aprobadas.

### P1. Biblioteca de conocimiento para IA

Organizar requerimientos históricos y estándares para permitir buscar **funcionalidades concretas**, no solo nombres de archivos.

- Mantener los PDF originales como respaldo y evidencia.
- Crear un catálogo con identificador del requerimiento, módulo, funcionalidad, versión, estado de aprobación/vigencia, ubicación del documento y, cuando sea posible, páginas relevantes.
- Identificar patrones reutilizables y conservar las excepciones técnicas.
- Verificar la vigencia de cada referencia antes de reutilizarla.
- Al finalizar un requerimiento, incorporar a la biblioteca únicamente especificaciones validadas.

**Google Drive** es un repositorio candidato, **no una integración ya comprobada con todas las cuentas gratuitas de ChatGPT**. Puede utilizarse para conservar PDF y `.md`; la lectura directa desde ChatGPT dependerá de la integración efectivamente disponible. Como alternativa inicial, el analista puede seleccionar y adjuntar los Markdown pertinentes a una conversación.

### P2. Catálogo de componentes estandarizados

Catálogo con identificador, versión, comportamiento predeterminado, parámetros configurables y excepciones:

- **Visuales:** botones, campos de fechas, alertas, modales, filtros, tablas y paginación.
- **Funcionales:** consultas, registro/actualización, permisos, reportes y exportación.
- **Procesamiento:** importaciones masivas, validaciones, sincronización, auditoría y manejo de errores.

Un requerimiento podría **referenciar un componente estándar** y documentar únicamente los cambios particulares, sin repetir toda su descripción. **Reutilización no significa imponer un comportamiento idéntico cuando cambian las reglas de negocio.**

### P3. Asistente de IA especializado en análisis

Como primera prueba se contempla utilizar **ChatGPT gratuito** y archivos **Markdown** como contexto de consulta e instrucciones. Las funciones de asistencia propuestas son:

- Preparación de entrevistas y preguntas sobre impactos entre módulos.
- Organización del alcance y del checklist funcional.
- Búsqueda y adaptación controlada de referencias existentes.
- Redacción asistida de especificaciones y criterios de aceptación.
- Revisión de omisiones, contradicciones y referencias sin vigencia confirmada.

**Reglas de uso propuestas:** la IA no inventa tablas, campos, permisos ni políticas; identifica la información que falta; separa hallazgos de propuestas; indica fuentes y niveles de certeza; el analista aprueba las decisiones funcionales y técnicas. Los archivos `.md` **no entrenan automáticamente** al modelo ni garantizan memoria permanente: deben proporcionarse o mantenerse accesibles por una vía compatible.

## 5. Modelo central propuesto: cinco etapas

| Etapa | Propósito | Entregable esperado |
|---|---|---|
| **1. Levantamiento inicial** | Identificar necesidad, problema, dependencias y límites del trabajo. | Acta de alcance, socializaciones y aprobación del Product Owner. |
| **2. Análisis funcional** | Desglosar lo que el sistema debe hacer: procesos, reglas, validaciones y escenarios. | Checklist funcional con identificadores, estados y pendientes. |
| **3. Diseño de solución** | Detallar interfaces, estructuras, procesamiento e integraciones. | Especificaciones técnicas y funcionales enlazadas con el checklist. |
| **4. Documentación estructurada** | Ordenar, vincular y consolidar lo generado con plantillas. | Requerimiento principal y anexos relacionados. |
| **5. Validación del análisis** | Revisar alcance, coherencia, viabilidad y criterios de aceptación antes del desarrollo. | Requerimiento validado para desarrollo. |

### Etapa 1. Levantamiento inicial

**Propuesta de actividades:**

- Preparación previa del analista con información existente y preguntas orientadoras.
- Reuniones de socialización con el solicitante/Product Owner.
- Evaluación temprana de impactos y dependencias entre módulos. **Ejemplo a investigar, no dependencia confirmada para todos los casos:** resultados de Laboratorio frente a diagnósticos, órdenes, consumos y facturación.
- Elaboración de un **acta de alcance** con necesidad, objetivos, inclusiones, exclusiones, restricciones, sistemas afectados y pendientes.
- **Aprobación del Product Owner**, con registro de cambios posteriores.

**Punto de control propuesto:** no avanzar al diseño detallado sin saber qué se aprobó y qué queda por confirmar.

### Etapa 2. Análisis funcional

Construir una **lista de lo que se va a hacer**. Más que un checklist de casillas terminadas, se propone una matriz que contenga:

- Identificador único por funcionalidad, por ejemplo `RF-001`.
- Descripción de comportamiento esperado.
- Reglas de negocio y excepciones identificadas.
- Dependencias o módulos afectados.
- Estado: definido, pendiente o no aplica.
- Dudas para resolver con el Product Owner y posibles antecedentes reutilizables.

La IA puede sugerir casos omitidos, pero el analista debe verificar su aplicación. El checklist es el **hilo conductor** del análisis posterior.

### Etapa 3. Diseño de solución

Se propusieron **seis bloques de especificación**. No tienen que equivaler obligatoriamente a seis archivos físicos para todos los requerimientos:

| Bloque | Contenido |
|---|---|
| **Funcional** | Objetivos, alcance y reglas; enlace al acta y checklist. |
| **Interfaces** | Vistas, campos, botones, validaciones y referencias a componentes estandarizados. |
| **Base de datos** | Tablas, columnas, relaciones, restricciones y cambios previstos. |
| **Procesamiento** | Lógica de negocio, algoritmos, consultas, transacciones y operaciones. |
| **Integraciones** | API, servicios, parámetros, respuestas, errores y autenticación cuando aplique. |
| **Pruebas** | Casos, datos necesarios, resultados esperados y criterios de aceptación. |

**Mejora propuesta:** cada bloque debe vincularse a las funcionalidades del checklist; una regla de negocio no debe confundirse con el detalle de implementación.

### Etapa 4. Documentación estructurada

Orden sugerido del paquete documental:

1. Información general y registro de socializaciones del Product Owner.
2. Acta de alcance y aprobaciones.
3. Checklist funcional.
4. Objetivo del requerimiento.
5. Referencias a interfaces y componentes estandarizados.
6. Referencias al diseño de base de datos.
7. **Documento principal:** procesamiento y reglas específicas de negocio.
8. **Integraciones**, cuando existan, con sus especificaciones técnicas.
9. **Pruebas y criterios de aceptación** verificables.

La propuesta **no exige duplicar el contenido completo de cada anexo en el principal**. Se plantea referenciar los documentos/identificadores y consolidar automáticamente el índice o paquete final mediante plantillas o una herramienta de generación.

**Trazabilidad ilustrativa:** `RF-005` (funcionalidad) → `RN-012` (regla de negocio) → `CP-018` (caso de prueba). Estos códigos son **ejemplos propuestos**, no identificadores existentes confirmados.

### Etapa 5. Validación del análisis

**Antes de desarrollar:** revisión funcional y técnica para identificar lagunas, contradicciones, integraciones no definidas, reglas sin pruebas o cambios fuera del alcance. La IA puede ayudar a revisar, pero no aprueba por sí sola.

**Distinguir de la verificación posterior al desarrollo:** después de implementar, un validador técnico podría comprobar convenciones, generar observaciones sustentadas en archivos y reglas y apoyar una devolución técnica. El desarrollador también debería aportar evidencia de pruebas funcionales, de integración y de aceptación. Un validador estático de código **no prueba automáticamente** todas las reglas de negocio.

## 6. Ideas transversales para mejorar la propuesta

1. **Matriz de impacto entre módulos:** mantener relaciones conocidas para preparar preguntas y detectar efectos secundarios; validar cada relación, no asumirla.
2. **Control de cambios:** diferenciar aclaraciones de nuevas funcionalidades, registrar responsable, motivo e impacto.
3. **Reutilización versionada:** ningún componente o antecedente debe considerarse universal sin revisar vigencia y excepciones.
4. **Trazabilidad:** relacionar alcance → funcionalidad → regla → especificación → prueba → evidencia.
5. **Medición del piloto:** tiempo de documentación, cantidad de aclaraciones de desarrollo, correcciones posteriores, reutilización efectiva y cobertura de pruebas.
6. **Seguridad de la información:** no incorporar información clínica identificable, credenciales ni datos de clientes a una cuenta gratuita sin autorización y revisión de controles de datos.

## 7. Esquema de flujo resumido

```text
PREPARACIÓN (propuesta)
  Biblioteca histórica + catálogo de componentes + configuración IA
                              |
                              v
1. LEVANTAMIENTO --> acta de alcance y socializaciones aprobadas
                              |
                              v
2. ANÁLISIS FUNCIONAL --> checklist de funcionalidades y pendientes
                              |
                              v
3. DISEÑO DE SOLUCIÓN --> bloques de interfaces, BD, lógica, API y pruebas
                              |
                              v
4. DOCUMENTACIÓN --> documento principal + anexos enlazados
                              |
                              v
5. VALIDACIÓN DEL ANÁLISIS --> revisión y aprobación para desarrollar
                              |
                              v
DESARROLLO --> verificación técnica y pruebas de aceptación
                              |
                              v
APRENDIZAJE --> actualización controlada de biblioteca y componentes
```

## 8. Estado de las decisiones

### Confirmado en conversación

- El proceso actual combina entrevistas con el cliente y reutilización/adaptación de requerimientos anteriores (**A y C**).
- La redacción detallada y las correcciones concentran gran parte del esfuerzo (**orden comunicado: C, D, E, B**).
- El analista interviene tanto en definiciones funcionales como técnicas.
- Se desea **preparar una propuesta**, sin afirmar todavía que sea la metodología adoptada.

### En evaluación, no implementado ni aprobado

- Arquitectura exacta de Google Drive, Markdown y acceso desde cuentas gratuitas.
- Cantidad de archivos y organización definitiva de la biblioteca.
- Catálogo de componentes, responsables de actualización y control de versiones.
- Formato final del acta, checklist, documentos técnicos y matriz de pruebas.
- Uso de un asistente IA y automatización de la consolidación documental.
- Alcance y tecnología del validador documental/técnico.
- Indicadores y resultados del piloto.

## 9. Guía para cualquier IA que lea este contexto

- Responder **en español** y utilizar la terminología de Dialisoft.
- Diferenciar explícitamente **información conocida**, **ejemplos ilustrativos** y **propuestas**.
- No afirmar que las etapas, catálogos, flujos o integraciones ya se implementaron.
- No deducir estructuras de base de datos, flujos clínicos ni reglas de negocio no demostradas por la fuente pertinente.
- Ante una consulta sobre un requerimiento concreto, solicitar o consultar la **fuente original actualizada** antes de describir detalles que aquí no aparecen.
- Priorizar la reducción de redacción repetitiva y del reproceso sin sacrificar la trazabilidad de la implementación y las pruebas.
- Un documento Markdown es un **resumen operacional**, no sustituye el contenido técnico completo de los PDF.

## 10. Fuentes que fundamentan este resumen

**Conversación:** respuestas del usuario sobre proceso A+C, orden de esfuerzo C-D-E-B, alcance del analista, arquitectura con biblioteca/componentes, cinco etapas, IA gratuita y validación.

**Documentos disponibles y parcialmente consultados:**

1. `RQ0002024 - Implementar consulta, importación y reporte de glosas SIIFA en Glosas y Devoluciones.pdf` — páginas 8–9 (alcance/BD), 89–90 (revalidaciones), 235–236 (reporte/permiso), entre otras partes descritas en su índice.
2. `Manual Programación Reingeniería 4.0 SQL.pdf` — secciones de políticas y optimizaciones.
3. `Manual Programación Reingeniería 4.0 PHP.pdf` — secciones de vistas, controladores y modelos.
4. `Manual Programación Reingeniería 4.0 JS.pdf` — secciones de variables y funciones/peticiones.
5. `Abreviaciones DESARROLLO DIALISOFT.xlsx` y `Abreviaciones DIALISOFT.xlsx` — identificados como recursos disponibles, sin reproducir aquí su contenido interno.

> **Nota de trazabilidad:** este archivo no demuestra que la IA tenga acceso posterior a todos esos originales. Para verificaciones técnicas detalladas deben volver a consultarse los documentos completos.
