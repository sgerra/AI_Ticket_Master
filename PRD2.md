# PRD-001: AI Ticket Manager — gestión centralizada de tickets con sugerencias de IA revisadas por personas

**Versión:** 2.0  
**Estado:** Borrador para entrega  
**Tipo:** Proyecto final — AI Builders

---

## Contexto y Problema

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

### Personas

> Las personas descriptas son **ficticias** y representan roles; no corresponden a empleados reales.

#### María — Mesa de Ayuda (rol: Mesa de Ayuda)

Es quien recibe gran parte de los pedidos realizados por los usuarios.

Actualmente recibe pedidos principalmente por mail y debe interpretar cada solicitud para determinar a quién corresponde derivarla.

Con el nuevo sistema utilizará la IA como ayuda para clasificar y asignar los tickets, y consultará los reportes.

#### Marcelo — Administrativo de Contable (rol: Solicitante)

Es un usuario de un área administrativa.

Realiza consultas y solicitudes relacionadas con los sistemas que utiliza su área.

Necesita poder registrar un pedido, consultar su estado y agregar información o comentarios cuando sea necesario.

#### Pedro — Desarrollador (rol: Desarrollador)

Es responsable de analizar y resolver los tickets que le son asignados.

Necesita recibir pedidos con información suficiente y poder consultar antecedentes de problemas similares.

---

## Objetivos

### Objetivo general

Centralizar la gestión de solicitudes de la empresa y utilizar IA para asistir a las personas que analizan y gestionan los tickets.

### Objetivos específicos

- Centralizar en un único sistema los pedidos que hoy llegan por mail y reuniones, que se registran como tickets desde la aplicación.
- Facilitar el seguimiento del estado de cada pedido.
- Reducir el tiempo necesario para clasificar y asignar tickets.
- Detectar información faltante antes de comenzar el análisis.
- Aprovechar el historial de tickets para encontrar problemas similares.
- Permitir que los usuarios puedan aceptar, modificar o rechazar las sugerencias realizadas por la IA.
- Mantener la decisión final siempre en manos de una persona.

### Meta de éxito

El tiempo promedio desde que un ticket se crea (estado **Nuevo**) hasta que pasa a **Asignado** es **menor a 1 día hábil** (hoy: varios días). Un día hábil equivale a la duración de la jornada configurada en RF-30. Se mide con el reporte de RF-27.

---

## Requerimientos Funcionales

### Valores predefinidos

- **Categorías:** Accesos, Permisos, Impresión, Error de sistema, Facturación, Consulta contable, Nuevo reporte, Cambio de funcionalidad, Consulta de proceso, Incidente.
- **Prioridades:** Alta, Media, Baja.
- **Áreas:** Mesa de Ayuda, Desarrollo, Infraestructura, Contable.
- **Roles:** Solicitante, Mesa de Ayuda, Desarrollador.
- **Datos requeridos de un ticket:** sistema afectado; qué ocurre o qué se pide; desde cuándo ocurre.

### RF-01 — Crear ticket

El sistema debe permitir a un usuario crear un ticket ingresando como mínimo un título y una descripción. Todo ticket nuevo comienza en estado **Nuevo**.

### RF-02 — Consultar ticket

El sistema debe permitir a un usuario consultar un ticket y visualizar su información y estado actual.

### RF-03 — Agregar comentarios

El sistema debe permitir a los usuarios agregar comentarios a un ticket existente.

### RF-04 — Definir categoría

El sistema debe permitir clasificar un ticket con una de las categorías predefinidas.

### RF-05 — Analizar ticket con IA

El sistema debe permitir solicitar un análisis de un ticket mediante inteligencia artificial.

### RF-06 — Sugerir categoría

El sistema debe sugerir, mediante IA, una de las categorías predefinidas a partir del contenido del ticket.

### RF-07 — Sugerir prioridad

El sistema debe sugerir, mediante IA, una de las prioridades predefinidas a partir del contenido del ticket.

### RF-08 — Sugerir área responsable

El sistema debe sugerir, mediante IA, una de las áreas predefinidas como responsable de la atención del ticket.

### RF-09 — Detectar información faltante

El sistema debe indicar, mediante IA, cuáles de los datos requeridos de un ticket no figuran en su título ni en su descripción.

### RF-10 — Buscar tickets similares

El sistema debe mostrar, para un texto ingresado por el usuario, hasta **5** tickets anteriores con contenido similar, ordenados de mayor a menor similitud, considerando únicamente los tickets que el usuario puede ver según RF-21 a RF-23.

### RF-11 — Aceptar sugerencia de IA

El sistema debe permitir al usuario aceptar una sugerencia realizada por la IA.

### RF-12 — Modificar sugerencia de IA

El sistema debe permitir al usuario modificar una sugerencia realizada por la IA antes de guardarla.

### RF-13 — Rechazar sugerencia de IA

El sistema debe permitir al usuario rechazar una sugerencia realizada por la IA.

### RF-14 — Cambiar estado del ticket

El sistema debe permitir cambiar el estado de un ticket únicamente según estas transiciones:

| Desde | Hacia |
|---|---|
| Nuevo | En análisis |
| En análisis | Asignado (solo si el ticket tiene área y responsable) |
| En análisis | Pendiente de información |
| Asignado | En progreso |
| En progreso | Pendiente de información |
| En progreso | Resuelto |
| Pendiente de información | El estado desde el que llegó (En análisis o En progreso) |
| Resuelto | Cerrado |
| Cerrado | En análisis (reapertura, RF-19) |

### RF-15 — Asignar área

El sistema debe permitir asignar un ticket a un área responsable.

### RF-16 — Asignar responsable

El sistema debe permitir asignar un ticket a un usuario responsable.

### RF-17 — Resolver ticket

El sistema debe permitir que el responsable del ticket o un usuario con rol Mesa de Ayuda marque un ticket como resuelto indicando una descripción de la solución.

### RF-18 — Cerrar ticket

El sistema debe permitir cerrar un ticket que se encuentre en estado Resuelto.

### RF-19 — Reabrir ticket

El sistema debe permitir reabrir un ticket cerrado, que pasa al estado **En análisis**.

### RF-20 — Asignar prioridad

El sistema debe permitir asignar a un ticket una de las prioridades predefinidas sin utilizar la IA.

### RF-21 — Visibilidad del Solicitante

El sistema debe mostrar a un usuario con rol Solicitante únicamente los tickets que él creó.

### RF-22 — Visibilidad del Desarrollador

El sistema debe mostrar a un usuario con rol Desarrollador únicamente los tickets que creó, los asignados a él y los asignados a cualquiera de las áreas a las que pertenece.

### RF-23 — Visibilidad de Mesa de Ayuda

El sistema debe mostrar a un usuario con rol Mesa de Ayuda todos los tickets.

### RF-24 — Reporte de tickets por estado

El sistema debe mostrar la cantidad de tickets en cada estado.

### RF-25 — Reporte de tickets por área

El sistema debe mostrar la cantidad de tickets por área responsable.

### RF-26 — Reporte de tickets por categoría

El sistema debe mostrar la cantidad de tickets por categoría.

### RF-27 — Reporte de tiempo de clasificación

El sistema debe mostrar el tiempo promedio, en horas hábiles según el horario configurado en RF-30, desde que un ticket se crea hasta que pasa al estado Asignado.

### RF-28 — Acceso a reportes

El sistema debe permitir el acceso a los reportes (RF-24 a RF-27) únicamente a usuarios con rol Mesa de Ayuda.

### RF-29 — Permisos por rol

El sistema debe permitir cada acción, sobre los tickets que el usuario puede ver, únicamente a los roles indicados en esta matriz:

| Acción | Solicitante | Mesa de Ayuda | Desarrollador |
|---|---|---|---|
| Crear ticket | ✓ | ✓ | ✓ |
| Consultar y comentar | ✓ | ✓ | ✓ |
| Analizar con IA | ✗ | ✓ | ✓ |
| Aceptar, modificar o rechazar sugerencias | ✗ | ✓ | ✓ |
| Buscar tickets similares | ✓ | ✓ | ✓ |
| Definir categoría y prioridad | ✗ | ✓ | ✓ |
| Asignar área y responsable | ✗ | ✓ | ✗ |
| Cambiar estado | ✗ | ✓ | ✓ (solo tickets asignados a él) |
| Resolver | ✗ | ✓ | ✓ (solo tickets asignados a él) |
| Cerrar | ✗ | ✓ | ✗ |
| Reabrir | ✓ (solo tickets propios) | ✓ | ✗ |

### RF-30 — Configurar horario hábil

El sistema debe permitir a un usuario con rol Mesa de Ayuda configurar los días hábiles de la semana y el horario de inicio y fin de la jornada. El valor inicial es **lunes a viernes, de 9 a 18 h**.

---

## Requerimientos No Funcionales

### RNF-01 — Tiempo de respuesta de IA

El análisis de un ticket mediante IA debe devolver una respuesta en un máximo de **10 segundos en al menos el 95% de las solicitudes**.

### RNF-02 — Historial de tickets

La búsqueda de tickets similares debe soportar inicialmente un historial mínimo de **100 tickets**.

### RNF-03 — Tiempo de búsqueda

La búsqueda de tickets similares debe devolver los resultados en un máximo de **5 segundos en al menos el 95% de las búsquedas, para un historial de hasta 10.000 tickets**.

### RNF-04 — Seguridad de API Key

La API Key utilizada para acceder al servicio de IA **no debe almacenarse ni exponerse en el frontend**.

### RNF-05 — Disponibilidad de IA

Si el servicio de IA no está disponible o no responde, el sistema debe permitir igualmente **crear, consultar, modificar y gestionar tickets**.

### RNF-06 — Control de sugerencias

Las sugerencias generadas por IA deben quedar identificadas como sugerencias y no deben modificar automáticamente la información definitiva del ticket.

### RNF-07 — Registro de decisiones

El sistema debe registrar si una sugerencia de IA fue **aceptada, modificada o rechazada** por el usuario.

### RNF-08 — Tiempo de respuesta general

Crear un ticket, consultar un ticket y cambiar su estado deben responder en un máximo de **3 segundos en al menos el 95% de las solicitudes**.

### RNF-09 — Calidad de las sugerencias de IA

Sobre el conjunto de prueba de **30 tickets** etiquetados a mano (D-05), la categoría, la prioridad y el área sugeridas deben coincidir con la etiqueta esperada en **al menos el 80%** de los casos (**≥ 24 de 30**), medido por separado para cada una.

### RNF-10 — Datos enviados a la IA

Al servicio de IA se envían **únicamente el título y la descripción** del ticket: **0** comentarios, nombres de usuario, correos electrónicos u otros datos del solicitante.

---

## Criterios de Aceptación

Los criterios de aceptación se expresan en **Gherkin en español**. Cada encabezado indica el requerimiento que verifica.

### AC-01 (RF-01) — Crear un ticket

```gherkin
# language: es
Característica: Crear un ticket

  Escenario: Ticket creado en estado Nuevo
    Dado que el usuario está autenticado
    Y se encuentra en la pantalla de creación de tickets
    Cuando ingresa el título "No puedo ingresar al sistema"
    Y ingresa la descripción "El sistema indica que mi usuario está bloqueado"
    Y presiona "Crear"
    Entonces existe un ticket nuevo con un identificador asignado
    Y su título es "No puedo ingresar al sistema"
    Y su descripción es "El sistema indica que mi usuario está bloqueado"
    Y su creador es el usuario autenticado
    Y su estado es "Nuevo"
```

### AC-02 (RF-02) — Consultar el estado

```gherkin
# language: es
Característica: Consultar ticket

  Escenario: Consultar el estado de un ticket
    Dado que existe un ticket en estado "En análisis"
    Cuando el usuario consulta el ticket
    Entonces el sistema debe mostrar el estado "En análisis"
```

### AC-03 (RF-03) — Agregar comentario

```gherkin
# language: es
Característica: Comentarios

  Escenario: Agregar un comentario a un ticket
    Dado que existe un ticket
    Cuando el usuario agrega el comentario "El problema continúa"
    Entonces el comentario debe quedar asociado al ticket
```

### AC-04 (RF-06) — Sugerir categoría

```gherkin
# language: es
Característica: Clasificación mediante IA

  Escenario: Clasificar un problema de acceso
    Dado que existe un ticket con la descripción
      "No puedo entrar al sistema, me dice usuario bloqueado"
    Cuando el usuario solicita analizar el ticket con IA
    Entonces la categoría sugerida debe ser "Accesos"
```

### AC-05 (RF-07) — Sugerir prioridad

```gherkin
# language: es
Característica: Sugerencia de prioridad

  Escenario: Sugerir prioridad para un problema que impide trabajar
    Dado que existe un ticket con la descripción
      "El sistema está caído y ningún usuario puede trabajar"
    Cuando el usuario solicita analizar el ticket con IA
    Entonces la prioridad sugerida debe ser "Alta"
```

### AC-06 (RF-08) — Sugerir área

```gherkin
# language: es
Característica: Sugerencia de área

  Escenario: Sugerir área responsable
    Dado que existe un ticket con la descripción
      "Necesito modificar el formato de un reporte contable"
    Cuando el usuario solicita analizar el ticket con IA
    Entonces el área sugerida debe ser "Desarrollo"
```

### AC-07 (RF-09) — Detectar información faltante

```gherkin
# language: es
Característica: Detección de información faltante

  Escenario: Detectar información necesaria
    Dado que existe un ticket con la descripción
      "No funciona el sistema"
    Cuando el usuario solicita analizar el ticket con IA
    Entonces el sistema debe indicar que falta información
    Y debe solicitar al menos el nombre del sistema afectado
```

### AC-08 (RF-10) — Buscar tickets similares

```gherkin
# language: es
Característica: Búsqueda de tickets similares

  Escenario: Encontrar un ticket relacionado
    Dado que existen al menos 100 tickets históricos
    Y existe un ticket histórico con la descripción
      "Usuario bloqueado al intentar ingresar al sistema"
    Cuando se busca un ticket similar a
      "No puedo entrar al sistema porque mi usuario está bloqueado"
    Entonces el sistema debe mostrar como máximo 5 resultados
    Y el ticket histórico debe aparecer entre esos 5 resultados
```

### AC-09 (RF-11) — Aceptar sugerencia

```gherkin
# language: es
Característica: Gestión de sugerencias de IA

  Escenario: Aceptar una categoría sugerida
    Dado que la IA sugirió la categoría "Accesos"
    Cuando el usuario acepta la sugerencia
    Entonces la categoría del ticket debe quedar como "Accesos"
    Y la sugerencia debe quedar registrada como "Aceptada"
```

### AC-10 (RF-12) — Modificar sugerencia

```gherkin
# language: es
Característica: Gestión de sugerencias de IA

  Escenario: Modificar una categoría sugerida
    Dado que la IA sugirió la categoría "Accesos"
    Cuando el usuario cambia la categoría a "Incidente"
    Y confirma el cambio
    Entonces la categoría del ticket debe quedar como "Incidente"
    Y la sugerencia debe quedar registrada como "Modificada"
```

### AC-11 (RF-13) — Rechazar sugerencia

```gherkin
# language: es
Característica: Gestión de sugerencias de IA

  Escenario: Rechazar una sugerencia
    Dado que la IA sugirió la categoría "Accesos"
    Cuando el usuario rechaza la sugerencia
    Entonces la categoría sugerida no debe modificar la categoría actual del ticket
    Y la sugerencia debe quedar registrada como "Rechazada"
```

### AC-12 (RF-14, RF-18) — Ciclo de vida

```gherkin
# language: es
Característica: Ciclo de vida del ticket

  Escenario: Avanzar un ticket hasta su cierre
    Dado que existe un ticket en estado "Nuevo"
    Cuando el usuario cambia su estado a "En análisis"
    Entonces el estado debe ser "En análisis"

    Cuando el usuario asigna el área "Desarrollo" y el responsable "D1"
    Y cambia el estado a "Asignado"
    Entonces el estado debe ser "Asignado"

    Cuando el responsable cambia el estado a "En progreso"
    Entonces el estado debe ser "En progreso"

    Cuando el responsable marca el ticket como "Resuelto"
    Entonces el estado debe ser "Resuelto"

    Cuando el usuario cierra el ticket
    Entonces el estado debe ser "Cerrado"
```

### AC-13 (RF-19) — Reabrir ticket

```gherkin
# language: es
Característica: Reapertura de tickets

  Escenario: Reabrir un ticket cerrado
    Dado que existe un ticket en estado "Cerrado"
    Cuando el usuario selecciona "Reabrir"
    Entonces el estado del ticket debe cambiar a "En análisis"
```

### AC-14 (RNF-05) — IA no disponible

```gherkin
# language: es
Característica: Disponibilidad del servicio de IA

  Escenario: El servicio de IA no responde
    Dado que existe un ticket en estado "Nuevo"
    Y el servicio de IA no está disponible
    Cuando el usuario intenta analizar el ticket
    Entonces el sistema debe informar que el análisis no está disponible

    Cuando el usuario agrega el comentario "Se revisa sin IA"
    Y cambia el estado del ticket de "Nuevo" a "En análisis"
    Entonces el comentario debe quedar asociado al ticket
    Y el estado del ticket debe ser "En análisis"
```

### AC-15 (RF-20) — Asignar prioridad sin IA

```gherkin
# language: es
Característica: Prioridad manual

  Escenario: Asignar prioridad a un ticket sin analizarlo con IA
    Dado que existe un ticket sin prioridad
    Y no se solicitó un análisis con IA para ese ticket
    Cuando el usuario asigna la prioridad "Media"
    Entonces la prioridad del ticket debe ser "Media"
```

### AC-16 (RF-21) — Solicitante ve solo sus tickets

```gherkin
# language: es
Característica: Control de acceso del Solicitante

  Antecedentes:
    Dado que el Solicitante "S1" creó el ticket "T1"
    Y el Solicitante "S2" creó el ticket "T2"

  Escenario: El listado muestra solo los tickets propios
    Cuando "S1" consulta su listado de tickets
    Entonces el listado debe contener "T1"
    Y el listado no debe contener "T2"

  Escenario: Acceso directo a un ticket ajeno
    Cuando "S1" intenta abrir "T2" por su identificador
    Entonces el sistema debe denegar el acceso
    Y no debe mostrar ningún dato de "T2"
```

### AC-17 (RF-22) — Desarrollador ve solo tickets propios, asignados a él o a su área

```gherkin
# language: es
Característica: Control de acceso del Desarrollador

  Escenario: El listado muestra solo los tickets propios, asignados a él o a su área
    Dado que el Desarrollador "D1" pertenece únicamente al área "Desarrollo"
    Y el ticket "T1" está asignado a "D1"
    Y el ticket "T2" está asignado al área "Desarrollo" sin responsable
    Y el ticket "T3" está asignado al área "Infraestructura" y no lo creó "D1"
    Y "D1" creó el ticket "T4", asignado al área "Contable"
    Cuando "D1" consulta su listado de tickets
    Entonces el listado debe contener "T1", "T2" y "T4"
    Y el listado no debe contener "T3"
```

### AC-18 (RF-23) — Mesa de Ayuda ve todos los tickets

```gherkin
# language: es
Característica: Control de acceso de Mesa de Ayuda

  Escenario: El listado muestra todos los tickets
    Dado que existen los tickets "T1", "T2" y "T3" creados por distintos Solicitantes
    Cuando un usuario con rol Mesa de Ayuda consulta el listado de tickets
    Entonces el listado debe contener "T1", "T2" y "T3"
```

### AC-19 (RF-24) — Reporte por estado

```gherkin
# language: es
Característica: Reportes

  Escenario: Cantidad de tickets por estado
    Dado que existen 3 tickets en estado "Nuevo" y 2 en estado "Asignado"
    Y no existen tickets en otros estados
    Cuando un usuario con rol Mesa de Ayuda abre el reporte por estado
    Entonces el reporte debe mostrar "Nuevo: 3" y "Asignado: 2"
    Y debe mostrar 0 para cada uno de los demás estados
```

### AC-20 (RF-25) — Reporte por área

```gherkin
# language: es
Característica: Reportes

  Escenario: Cantidad de tickets por área
    Dado que existen 4 tickets del área "Desarrollo" y 1 del área "Contable"
    Y no existen tickets de otras áreas
    Cuando un usuario con rol Mesa de Ayuda abre el reporte por área
    Entonces el reporte debe mostrar "Desarrollo: 4" y "Contable: 1"
    Y debe mostrar 0 para cada una de las demás áreas
```

### AC-21 (RF-26) — Reporte por categoría

```gherkin
# language: es
Característica: Reportes

  Escenario: Cantidad de tickets por categoría
    Dado que existen 2 tickets de la categoría "Accesos" y 3 de "Facturación"
    Y no existen tickets de otras categorías
    Cuando un usuario con rol Mesa de Ayuda abre el reporte por categoría
    Entonces el reporte debe mostrar "Accesos: 2" y "Facturación: 3"
    Y debe mostrar 0 para cada una de las demás categorías
```

### AC-22 (RF-27) — Reporte de tiempo de clasificación

```gherkin
# language: es
Característica: Reportes

  Escenario: Tiempo promedio hasta la asignación
    Dado que el ticket "T1" pasó de "Nuevo" a "Asignado" en 4 horas hábiles
    Y el ticket "T2" pasó de "Nuevo" a "Asignado" en 8 horas hábiles
    Y no existen otros tickets asignados
    Cuando un usuario con rol Mesa de Ayuda abre el reporte de tiempo de clasificación
    Entonces el reporte debe mostrar un promedio de 6 horas hábiles
```

### AC-23 (RF-28) — Acceso a reportes restringido

```gherkin
# language: es
Característica: Control de acceso a reportes

  Esquema del escenario: Un rol distinto de Mesa de Ayuda no accede a los reportes
    Dado que el usuario tiene rol "<rol>"
    Cuando intenta abrir cualquiera de los reportes
    Entonces el sistema debe denegar el acceso
    Y no debe mostrar ningún dato del reporte

    Ejemplos:
      | rol           |
      | Solicitante   |
      | Desarrollador |
```

### AC-24 (RNF-09) — Calidad de las sugerencias de IA

```gherkin
# language: es
Característica: Calidad de las sugerencias de IA

  Escenario: Evaluación sobre el conjunto de prueba
    Dado un conjunto de prueba de 30 tickets con categoría, prioridad y área esperadas
    Cuando se analiza cada ticket con IA
    Entonces al menos 24 categorías sugeridas deben coincidir con la esperada
    Y al menos 24 prioridades sugeridas deben coincidir con la esperada
    Y al menos 24 áreas sugeridas deben coincidir con la esperada
```

### AC-25 (RF-04) — Definir categoría

```gherkin
# language: es
Característica: Categoría manual

  Escenario: Asignar una categoría predefinida
    Dado que existe un ticket sin categoría
    Cuando un usuario con rol Mesa de Ayuda asigna la categoría "Impresión"
    Entonces la categoría del ticket debe ser "Impresión"
```

### AC-26 (RF-05) — Solicitar análisis con IA

```gherkin
# language: es
Característica: Análisis con IA

  Escenario: Solicitar el análisis de un ticket
    Dado que existe un ticket sin categoría, prioridad ni área
    Cuando un usuario con rol Mesa de Ayuda solicita analizar el ticket con IA
    Entonces el sistema debe mostrar una categoría, una prioridad y un área sugeridas, identificadas como sugerencias
    Y el ticket debe seguir sin categoría, prioridad ni área
```

### AC-27 (RF-15) — Asignar área

```gherkin
# language: es
Característica: Asignación

  Escenario: Asignar un área responsable
    Dado que existe un ticket en estado "En análisis" sin área
    Cuando un usuario con rol Mesa de Ayuda asigna el área "Infraestructura"
    Entonces el área del ticket debe ser "Infraestructura"
```

### AC-28 (RF-16) — Asignar responsable

```gherkin
# language: es
Característica: Asignación

  Escenario: Asignar un usuario responsable
    Dado que existe un ticket en estado "En análisis" sin responsable
    Y existe el Desarrollador "D1"
    Cuando un usuario con rol Mesa de Ayuda asigna el ticket a "D1"
    Entonces el responsable del ticket debe ser "D1"
```

### AC-29 (RF-17) — Resolver ticket

```gherkin
# language: es
Característica: Resolución

  Antecedentes:
    Dado que el ticket "T1" está en estado "En progreso"
    Y está asignado al Desarrollador "D1"

  Escenario: Resolver con descripción de la solución
    Cuando "D1" marca "T1" como resuelto con la descripción "Se desbloqueó el usuario"
    Entonces el estado de "T1" debe ser "Resuelto"
    Y la solución de "T1" debe ser "Se desbloqueó el usuario"

  Escenario: Resolver sin descripción de la solución
    Cuando "D1" intenta marcar "T1" como resuelto sin descripción
    Entonces el sistema debe rechazar la acción
    Y el estado de "T1" debe seguir siendo "En progreso"
```

### AC-30 (RF-10) — La búsqueda de similares respeta la visibilidad

```gherkin
# language: es
Característica: Control de acceso en la búsqueda de similares

  Escenario: Un Solicitante no ve tickets ajenos en la búsqueda
    Dado que el Solicitante "S2" creó el ticket "T2" con la descripción
      "Usuario bloqueado al intentar ingresar al sistema"
    Y el Solicitante "S1" no creó "T2"
    Cuando "S1" busca tickets similares a
      "No puedo entrar al sistema porque mi usuario está bloqueado"
    Entonces "T2" no debe aparecer entre los resultados
```

### AC-31 (RF-29) — Permisos por rol

```gherkin
# language: es
Característica: Permisos por rol

  Esquema del escenario: Acción no permitida para el rol
    Dado que el usuario tiene rol "<rol>"
    Y puede ver el ticket "T1" en estado "<estado>"
    Cuando intenta "<acción>" sobre "T1"
    Entonces el sistema debe denegar la acción
    Y "T1" no debe cambiar

    Ejemplos:
      | rol           | estado      | acción                                  |
      | Solicitante   | Nuevo       | analizar con IA                         |
      | Solicitante   | Nuevo       | cambiar el estado a "En análisis"       |
      | Desarrollador | En análisis | asignar el área "Infraestructura"       |
      | Desarrollador | Resuelto    | cerrar el ticket                        |
      | Desarrollador | Asignado    | cambiar el estado a "En progreso" de un ticket asignado a otro Desarrollador de su área |

  Escenario: El Solicitante reabre su propio ticket
    Dado que el Solicitante "S1" creó el ticket "T1"
    Y "T1" está en estado "Cerrado"
    Cuando "S1" reabre "T1"
    Entonces el estado de "T1" debe ser "En análisis"
```

### AC-32 (RF-30) — Configurar horario hábil

```gherkin
# language: es
Característica: Horario hábil

  Escenario: El horario configurado se usa en el reporte de tiempo de clasificación
    Dado que un usuario con rol Mesa de Ayuda configura los días hábiles de lunes a viernes y el horario de 9 a 17 h
    Y el ticket "T1" se creó un lunes a las 16 h
    Y pasó a "Asignado" el martes siguiente a las 10 h
    Y no existen otros tickets asignados
    Cuando un usuario con rol Mesa de Ayuda abre el reporte de tiempo de clasificación
    Entonces el reporte debe mostrar un promedio de 2 horas hábiles
```

### AC-33 (RF-14) — No se asigna sin área y responsable

```gherkin
# language: es
Característica: Ciclo de vida del ticket

  Esquema del escenario: Pasar a Asignado sin área o sin responsable
    Dado que existe un ticket en estado "En análisis"
    Y su área es "<área>"
    Y su responsable es "<responsable>"
    Cuando un usuario con rol Mesa de Ayuda intenta cambiar el estado a "Asignado"
    Entonces el sistema debe rechazar la acción
    Y el estado debe seguir siendo "En análisis"

    Ejemplos:
      | área       | responsable |
      | (ninguna)  | D1          |
      | Desarrollo | (ninguno)   |
      | (ninguna)  | (ninguno)   |
```

---

## Fuera de Alcance

Para limitar el alcance de la primera versión quedan fuera:

- Ingreso automático de pedidos por mail (creación de tickets a partir de correos).
- Notificaciones (por mail o dentro de la aplicación).
- Adjuntos en los tickets (archivos o capturas de pantalla).
- Métricas de uso de las sugerencias de IA (porcentaje de aceptadas, modificadas o rechazadas).
- Aviso al usuario previo al envío del contenido al servicio de IA.
- Configuración de feriados o fechas no hábiles.
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

## Riesgos y Dependencias

### Riesgos

#### R-01 — Clasificación incorrecta

La IA puede sugerir una categoría, prioridad o área incorrecta.

**Mitigación:** el usuario debe poder aceptar, modificar o rechazar cada sugerencia.

#### R-02 — Información incorrecta generada por IA

La IA podría generar información que no se encuentra en el ticket.

**Mitigación:** las respuestas de IA serán consideradas sugerencias y deberán ser revisadas por un usuario.

#### R-03 — Pocos datos históricos

La búsqueda de tickets similares puede perder utilidad si no existe suficiente información histórica.

**Mitigación:** utilizar inicialmente un conjunto de al menos 100 tickets de ejemplo (D-04).

#### R-04 — Indisponibilidad del servicio de IA

El proveedor de IA podría no responder o presentar una interrupción.

**Mitigación:** las funcionalidades principales de gestión de tickets deben continuar funcionando sin IA.

### Dependencias

#### D-01 — Servicio de IA

Las funcionalidades de análisis dependen de un servicio de inteligencia artificial accesible mediante API.

#### D-02 — Historial de tickets

La búsqueda de tickets similares depende de disponer de tickets históricos correctamente almacenados.

#### D-03 — Usuarios y permisos

El sistema depende de contar con usuarios y roles definidos para determinar quién puede crear, analizar, asignar, resolver y cerrar tickets (RF-29). Cada usuario tiene un rol y pertenece a una o más áreas.

#### D-04 — Datos iniciales para la demostración

Para demostrar la búsqueda de tickets similares desde la primera versión se utilizará un conjunto inicial de **100 tickets de ejemplo**, generados a partir de situaciones habituales, por ejemplo:

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

Estos datos se usan exclusivamente como información inicial para probar la funcionalidad durante el desarrollo del proyecto.

#### D-05 — Conjunto de prueba para la calidad de la IA

Para medir RNF-09 se toman **30 de los 100 tickets de ejemplo** (D-04). Un usuario con rol Mesa de Ayuda les asigna a mano la categoría, la prioridad y el área esperadas antes de la evaluación.
