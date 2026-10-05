# PRD — AI Ticket Manager

**Versión:** 1.0  
**Estado:** Borrador para entrega  
**Tipo:** Proyecto final — AI Builders

---

## 1. Contexto y problema

Actualmente, en la empresa los pedidos de soporte, consultas y desarrollos se gestionan principalmente por **mail y reuniones**.

En el sistema actual se reciben aproximadamente **50 pedidos por semana**. Estos pedidos son recibidos y clasificados principalmente por **Mesa de Ayuda o por los líderes de equipo**.

Una vez recibido un pedido, es necesario entender qué se está solicitando, determinar a qué área corresponde, definir su prioridad y asignarlo a la persona correspondiente. Este proceso puede demorar **varios días**, especialmente cuando el pedido no contiene toda la información necesaria o requiere consultar con otras personas.

Además, con el tiempo se genera un historial de pedidos que podría ser útil para resolver nuevos casos, pero actualmente encontrar un pedido anterior con un problema similar requiere realizar búsquedas manuales.

La propuesta es desarrollar **AI Ticket Manager**, un sistema de gestión de tickets que centralice estos pedidos y utilice inteligencia artificial como asistente para ayudar a analizarlos.

La IA podrá sugerir información como:

- Tipo o categoría del ticket.
- Prioridad.
- Área responsable.
- Información que falta para poder analizarlo.
- Tickets anteriores que podrían estar relacionados.

La decisión final siempre estará a cargo de una persona. La IA **no podrá modificar, cerrar ni resolver automáticamente un ticket**.

---

## 2. Personas

### María — Mesa de Ayuda

Es quien recibe gran parte de los pedidos realizados por los usuarios.

Actualmente recibe pedidos principalmente por mail y debe interpretar cada solicitud para determinar a quién corresponde derivarla.

Con el nuevo sistema utilizará la IA como ayuda para clasificar y asignar los tickets.

### Marcelo — Administrativo de Contable

Es un usuario de un área administrativa.

Realiza consultas y solicitudes relacionadas con los sistemas que utiliza su área.

Necesita poder registrar un pedido, consultar su estado y agregar información o comentarios cuando sea necesario.

### Pedro — Desarrollador

Es responsable de analizar y resolver los tickets que le son asignados.

Necesita recibir pedidos con información suficiente y poder consultar antecedentes de problemas similares.

---

## 3. Objetivos

### Objetivo general

Centralizar la gestión de solicitudes de la empresa y utilizar IA para asistir a las personas que analizan y gestionan los tickets.

### Objetivos específicos

- Centralizar los pedidos que actualmente llegan por diferentes medios.
- Facilitar el seguimiento del estado de cada pedido.
- Reducir el tiempo necesario para clasificar y asignar tickets.
- Detectar información faltante antes de comenzar el análisis.
- Aprovechar el historial de tickets para encontrar problemas similares.
- Permitir que los usuarios puedan aceptar, modificar o rechazar las sugerencias realizadas por la IA.
- Mantener la decisión final siempre en manos de una persona.

---

## 4. Alcance

La primera versión permitirá:

- Crear tickets.
- Consultar tickets.
- Agregar comentarios.
- Cambiar el estado de un ticket.
- Asignar área y responsable.
- Analizar tickets utilizando IA.
- Sugerir categoría.
- Sugerir prioridad.
- Sugerir área responsable.
- Detectar información faltante.
- Buscar tickets similares.
- Aceptar, modificar o rechazar las sugerencias de IA.
- Resolver, cerrar y reabrir tickets.

---

## 5. Requerimientos funcionales

### RF-01 — Crear ticket

El sistema debe permitir a un usuario crear un ticket ingresando como mínimo un título y una descripción.

### RF-02 — Consultar ticket

El sistema debe permitir a un usuario consultar un ticket y visualizar su información y estado actual.

### RF-03 — Agregar comentarios

El sistema debe permitir a los usuarios agregar comentarios a un ticket existente.

### RF-04 — Definir categoría

El sistema debe permitir clasificar un ticket utilizando categorías predefinidas.

### RF-05 — Analizar ticket con IA

El sistema debe permitir solicitar un análisis de un ticket mediante inteligencia artificial.

### RF-06 — Sugerir categoría

La IA debe analizar el contenido del ticket y sugerir una categoría.

### RF-07 — Sugerir prioridad

La IA debe analizar el contenido del ticket y sugerir una prioridad.

### RF-08 — Sugerir área responsable

La IA debe analizar el contenido del ticket y sugerir el área responsable de su atención.

### RF-09 — Detectar información faltante

La IA debe identificar información que podría ser necesaria para analizar o resolver el ticket.

### RF-10 — Buscar tickets similares

El sistema debe permitir buscar tickets anteriores que tengan contenido similar al ticket analizado.

### RF-11 — Aceptar sugerencia de IA

El sistema debe permitir al usuario aceptar una sugerencia realizada por la IA.

### RF-12 — Modificar sugerencia de IA

El sistema debe permitir al usuario modificar una sugerencia realizada por la IA antes de guardarla.

### RF-13 — Rechazar sugerencia de IA

El sistema debe permitir al usuario rechazar una sugerencia realizada por la IA.

### RF-14 — Estados del ticket

El sistema debe permitir gestionar los siguientes estados:

**Nuevo → En análisis → Pendiente de información → Asignado → En progreso → Resuelto → Cerrado**

El sistema también debe permitir **reabrir** un ticket cerrado.

### RF-15 — Asignar área

El sistema debe permitir asignar un ticket a un área responsable.

### RF-16 — Asignar responsable

El sistema debe permitir asignar un ticket a un usuario responsable.

### RF-17 — Resolver ticket

El sistema debe permitir que el responsable marque un ticket como resuelto indicando una descripción de la solución.

### RF-18 — Cerrar ticket

El sistema debe permitir cerrar un ticket que se encuentre en estado Resuelto.

### RF-19 — Reabrir ticket

El sistema debe permitir reabrir un ticket cerrado cuando sea necesario continuar con su atención.

---

## 6. Requerimientos no funcionales

### RNF-01 — Tiempo de respuesta de IA

El análisis de un ticket mediante IA debe devolver una respuesta en un máximo de **10 segundos en al menos el 95% de las solicitudes**.

### RNF-02 — Historial de tickets

La búsqueda de tickets similares debe soportar inicialmente un historial mínimo de **100 tickets**.

### RNF-03 — Tiempo de búsqueda

La búsqueda de tickets similares debe devolver los resultados en un máximo de **5 segundos para un historial de hasta 10.000 tickets**.

### RNF-04 — Seguridad de API Key

La API Key utilizada para acceder al servicio de IA **no debe almacenarse ni exponerse en el frontend**.

### RNF-05 — Disponibilidad de IA

Si el servicio de IA no está disponible o no responde, el sistema debe permitir igualmente **crear, consultar, modificar y gestionar tickets**.

### RNF-06 — Control de sugerencias

Las sugerencias generadas por IA deben quedar identificadas como sugerencias y no deben modificar automáticamente la información definitiva del ticket.

### RNF-07 — Registro de decisiones

El sistema debe registrar si una sugerencia de IA fue **aceptada, modificada o rechazada** por el usuario.

### RNF-08 — Tiempo de respuesta general

Las operaciones habituales del sistema, como consultar un ticket o cambiar su estado, deben responder en un máximo de **3 segundos en al menos el 95% de las solicitudes**.

---

## 7. Criterios de aceptación

Los criterios de aceptación se expresan utilizando **Gherkin**, buscando que cada escenario pueda determinarse como verdadero o falso.

### AC-01 — Crear un ticket

```gherkin
Feature: Crear un ticket

  Scenario: Crear un ticket correctamente
    Given que el usuario está autenticado
    And se encuentra en la pantalla de creación de tickets
    When ingresa el título "No puedo ingresar al sistema"
    And ingresa la descripción "El sistema indica que mi usuario está bloqueado"
    And presiona "Crear"
    Then el sistema debe crear el ticket
    And el ticket debe quedar en estado "Nuevo"
```

### AC-02 — Consultar el estado

```gherkin
Feature: Consultar ticket

  Scenario: Consultar el estado de un ticket
    Given que existe un ticket en estado "En análisis"
    When el usuario consulta el ticket
    Then el sistema debe mostrar el estado "En análisis"
```

### AC-03 — Agregar comentario

```gherkin
Feature: Comentarios

  Scenario: Agregar un comentario a un ticket
    Given que existe un ticket
    When el usuario agrega el comentario "El problema continúa"
    Then el comentario debe quedar asociado al ticket
```

### AC-04 — Sugerir categoría

```gherkin
Feature: Clasificación mediante IA

  Scenario: Clasificar un problema de acceso
    Given que existe un ticket con la descripción
      "No puedo entrar al sistema, me dice usuario bloqueado"
    When el usuario solicita analizar el ticket con IA
    Then la categoría sugerida debe ser "Accesos"
```

### AC-05 — Sugerir prioridad

```gherkin
Feature: Sugerencia de prioridad

  Scenario: Sugerir prioridad para un problema que impide trabajar
    Given que existe un ticket con la descripción
      "El sistema está caído y ningún usuario puede trabajar"
    When el usuario solicita analizar el ticket con IA
    Then la prioridad sugerida debe ser "Alta"
```

### AC-06 — Sugerir área

```gherkin
Feature: Sugerencia de área

  Scenario: Sugerir área responsable
    Given que existe un ticket con la descripción
      "Necesito modificar el formato de un reporte contable"
    When el usuario solicita analizar el ticket con IA
    Then el área sugerida debe ser "Desarrollo"
```

### AC-07 — Detectar información faltante

```gherkin
Feature: Detección de información faltante

  Scenario: Detectar información necesaria
    Given que existe un ticket con la descripción
      "No funciona el sistema"
    When el usuario solicita analizar el ticket con IA
    Then el sistema debe indicar que falta información
    And debe solicitar al menos el nombre del sistema afectado
```

### AC-08 — Buscar tickets similares

```gherkin
Feature: Búsqueda de tickets similares

  Scenario: Encontrar un ticket relacionado
    Given que existen al menos 100 tickets históricos
    And existe un ticket histórico con la descripción
      "Usuario bloqueado al intentar ingresar al sistema"
    When se busca un ticket similar a
      "No puedo entrar al sistema porque mi usuario está bloqueado"
    Then el ticket histórico debe aparecer entre los resultados
```

### AC-09 — Aceptar sugerencia

```gherkin
Feature: Gestión de sugerencias de IA

  Scenario: Aceptar una categoría sugerida
    Given que la IA sugirió la categoría "Accesos"
    When el usuario acepta la sugerencia
    Then la categoría del ticket debe quedar como "Accesos"
    And la sugerencia debe quedar registrada como "Aceptada"
```

### AC-10 — Modificar sugerencia

```gherkin
Feature: Gestión de sugerencias de IA

  Scenario: Modificar una categoría sugerida
    Given que la IA sugirió la categoría "Accesos"
    When el usuario cambia la categoría a "Incidente"
    And confirma el cambio
    Then la categoría del ticket debe quedar como "Incidente"
    And la sugerencia debe quedar registrada como "Modificada"
```

### AC-11 — Rechazar sugerencia

```gherkin
Feature: Gestión de sugerencias de IA

  Scenario: Rechazar una sugerencia
    Given que la IA sugirió la categoría "Accesos"
    When el usuario rechaza la sugerencia
    Then la categoría sugerida no debe modificar la categoría actual del ticket
    And la sugerencia debe quedar registrada como "Rechazada"
```

### AC-12 — Ciclo de vida

```gherkin
Feature: Ciclo de vida del ticket

  Scenario: Avanzar un ticket hasta su cierre
    Given que existe un ticket en estado "Nuevo"
    When el usuario cambia su estado a "En análisis"
    Then el estado debe ser "En análisis"

    When el usuario cambia el estado a "Asignado"
    Then el estado debe ser "Asignado"

    When el responsable marca el ticket como "Resuelto"
    Then el estado debe ser "Resuelto"

    When el usuario cierra el ticket
    Then el estado debe ser "Cerrado"
```

### AC-13 — Reabrir ticket

```gherkin
Feature: Reapertura de tickets

  Scenario: Reabrir un ticket cerrado
    Given que existe un ticket en estado "Cerrado"
    When el usuario selecciona "Reabrir"
    Then el estado del ticket debe cambiar a "En análisis"
```

### AC-14 — IA no disponible

```gherkin
Feature: Disponibilidad del servicio de IA

  Scenario: El servicio de IA no responde
    Given que existe un ticket
    And el servicio de IA no está disponible
    When el usuario intenta analizar el ticket
    Then el sistema debe informar que el análisis no está disponible
    And el usuario debe poder continuar gestionando el ticket
```

---

## 8. Datos iniciales para la demostración

Para poder demostrar la funcionalidad de búsqueda de tickets similares desde la primera versión, se utilizará un conjunto inicial de **100 tickets de ejemplo**.

Los tickets serán generados tomando como referencia situaciones habituales de la empresa, por ejemplo:

- Problemas de acceso.
- Usuarios bloqueados.
- Problemas de impresión.
- Errores en sistemas internos.
- Consultas contables.
- Problemas de facturación.
- Solicitudes de nuevos reportes.
- Cambios en funcionalidades existentes.
- Problemas de permisos.
- Consultas sobre procesos.

Estos datos serán utilizados exclusivamente como información inicial para probar la funcionalidad durante el desarrollo del proyecto.

---

## 9. Fuera de alcance inicial

Para limitar el alcance de la primera versión quedan fuera:

- Integración con WhatsApp.
- Integración con Telegram.
- Aplicación móvil.
- Integración automática con otros sistemas de la empresa.
- Creación automática de ramas de código.
- Modificación automática del código fuente.
- Resolución automática de tickets por parte de la IA.
- Cierre automático de tickets por parte de la IA.
- Envío automático de respuestas a usuarios sin revisión humana.

La IA podrá **sugerir**, pero la decisión final siempre deberá ser tomada por un usuario.

---

## 10. Riesgos y dependencias

### Riesgos

#### R-01 — Clasificación incorrecta

La IA puede sugerir una categoría, prioridad o área incorrecta.

**Mitigación:** el usuario debe poder aceptar, modificar o rechazar cada sugerencia.

#### R-02 — Información incorrecta generada por IA

La IA podría generar información que no se encuentra en el ticket.

**Mitigación:** las respuestas de IA serán consideradas sugerencias y deberán ser revisadas por un usuario.

#### R-03 — Pocos datos históricos

La búsqueda de tickets similares puede perder utilidad si no existe suficiente información histórica.

**Mitigación:** utilizar inicialmente un conjunto de al menos 100 tickets de ejemplo.

#### R-04 — Indisponibilidad del servicio de IA

El proveedor de IA podría no responder o presentar una interrupción.

**Mitigación:** las funcionalidades principales de gestión de tickets deben continuar funcionando sin IA.

### Dependencias

#### D-01 — Servicio de IA

Las funcionalidades de análisis dependen de un servicio de inteligencia artificial accesible mediante API.

#### D-02 — Historial de tickets

La búsqueda de tickets similares depende de disponer de tickets históricos correctamente almacenados.

#### D-03 — Usuarios y permisos

El sistema depende de contar con usuarios y roles definidos para determinar quién puede crear, analizar, asignar, resolver y cerrar tickets.

---

## 11. Reglas de negocio

### RN-01

Un ticket nuevo debe comenzar siempre en estado **Nuevo**.

### RN-02

La IA no puede modificar automáticamente los datos definitivos del ticket.

### RN-03

Una sugerencia de IA debe poder ser aceptada, modificada o rechazada por un usuario autorizado.

### RN-04

Un ticket solamente puede pasar a **Cerrado** después de haber sido marcado como **Resuelto**.

### RN-05

Un ticket cerrado puede ser reabierto.

### RN-06

Las acciones realizadas sobre las sugerencias de IA deben quedar registradas.

---

## 12. Trazabilidad

| Requerimiento | Criterio de aceptación |
|---|---|
| RF-01 Crear ticket | AC-01 |
| RF-02 Consultar ticket | AC-02 |
| RF-03 Agregar comentarios | AC-03 |
| RF-06 Sugerir categoría | AC-04 |
| RF-07 Sugerir prioridad | AC-05 |
| RF-08 Sugerir área | AC-06 |
| RF-09 Detectar información faltante | AC-07 |
| RF-10 Buscar tickets similares | AC-08 |
| RF-11 Aceptar sugerencia | AC-09 |
| RF-12 Modificar sugerencia | AC-10 |
| RF-13 Rechazar sugerencia | AC-11 |
| RF-14 Estados del ticket | AC-12 |
| RF-18 Cerrar ticket | AC-12 |
| RF-19 Reabrir ticket | AC-13 |
| RNF-05 Disponibilidad de IA | AC-14 |

---

## 13. Definición de terminado del PRD

El PRD se considera completo cuando:

- El problema está definido.
- Las personas involucradas están identificadas.
- Los objetivos están definidos.
- Los requerimientos funcionales están identificados.
- Los requerimientos no funcionales tienen métricas verificables.
- Cada requerimiento funcional tiene al menos un criterio de aceptación.
- Los criterios de aceptación están expresados en Gherkin.
- Los criterios permiten determinar un resultado verdadero o falso.
- El ciclo de vida del ticket está definido.
- El alcance está definido.
- El fuera de alcance está definido.
- Los riesgos y dependencias están identificados.
- Existe trazabilidad entre requerimientos y criterios de aceptación.
- Se dispone de datos iniciales para demostrar la búsqueda de tickets similares.
