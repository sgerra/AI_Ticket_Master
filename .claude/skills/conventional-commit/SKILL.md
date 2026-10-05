---
name: conventional-commit
description: Arma y ejecuta un commit de Git con formato Conventional Commits (tipo(scope): descripción en imperativo). Se usa cuando el usuario pide hacer un commit, commitear cambios o redactar un mensaje de commit.
---

# Conventional Commit

## Formato del mensaje

```
tipo(scope): descripción en imperativo
```

Ejemplos:

```
feat(auth): agregar validación de email en el registro
fix(tickets): rechazar tickets con asunto vacío
docs(prd): aclarar criterio de control de acceso
```

### Tipo (obligatorio)

Dice qué clase de cambio es:

| Tipo | Cuándo |
|---|---|
| `feat` | Feature nueva |
| `fix` | Arreglo de un error |
| `docs` | Documentación |
| `refactor` | Cambio de código que no agrega features ni arregla errores |
| `test` | Tests nuevos o modificados |
| `chore` | Mantenimiento (dependencias, configuración, scripts) |

No uses otros tipos.

### Scope (opcional)

Dice qué parte del proyecto toca, en minúscula y en una palabra: `auth`, `tickets`, `prd`, `ia`, `reportes`. Si el cambio no corresponde a una parte concreta, omitilo junto con los paréntesis: `chore: actualizar dependencias`.

### Descripción (obligatoria)

- En imperativo: "agregar", "corregir", "aclarar"; no "agregado", "agrega" ni "agregando".
- En minúscula, incluida la primera letra.
- Sin punto final.
- Corta: la primera línea completa (`tipo(scope): descripción`) tiene **72 caracteres o menos**.

## Pasos

1. **Revisar los cambios.** Corré `git status` y `git diff` (y `git diff --staged` si ya hay archivos agregados). Si no hay cambios, avisale al usuario y no hagas nada.
2. **Revisar datos sensibles.** Antes de commitear, buscá en el diff claves de API, tokens, contraseñas, archivos `.env` y datos personales o de clientes, empleados o proveedores. Si encontrás algo, no commitees: avisale al usuario qué encontraste y dónde.
3. **Un commit, un propósito.** Si los cambios mezclan propósitos distintos (por ejemplo, un `feat` y un `docs` sin relación), proponé separarlos en varios commits y preguntá antes de seguir.
4. **Elegir tipo y scope** a partir de lo que cambia el diff, no del nombre de los archivos.
5. **Redactar el mensaje** con el formato de arriba y verificar cada regla: tipo de la lista, imperativo, minúscula, sin punto final, ≤ 72 caracteres.
6. **Cuerpo (opcional).** Si el porqué del cambio no es obvio, agregá un cuerpo después de una línea en blanco, con líneas de hasta 72 caracteres. Respetá las líneas de atribución que pida el entorno (por ejemplo, `Co-Authored-By`) al final del mensaje.
7. **Agregar y commitear.** Agregá solo los archivos que corresponden al commit, por nombre (no uses `git add -A` ni `git add .`). Después corré `git commit`.
8. **Informar.** Mostrá el hash y el mensaje del commit. No hagas `git push` salvo que el usuario lo pida.
