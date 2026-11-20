---
name: commits-profesionales
description: Flujo de git profesional con Conventional Commits en español. Úsala siempre que se vaya a hacer un commit, crear una rama, abrir o fusionar un pull request, escribir un mensaje de merge, preparar un release o un CHANGELOG, o cuando pidan "haz commit", "sube los cambios", "abre un PR", "commits profesionales", "ordena el historial" o "conventional commits".
---

# Commits profesionales

El historial de git es documentación: quien lo lea en seis meses tiene que entender **qué** cambió y **por qué** sin abrir el diff.

## 1. Formato del mensaje

```
tipo(alcance): descripción corta

- por qué se hizo (opcional, viñetas cortas)
- qué queda pendiente o qué riesgo tiene

BREAKING CHANGE: qué deja de funcionar y cómo migrar (solo si aplica)
```

Reglas de la primera línea:
- Español, **imperativo** ("agregar", "corregir", no "agregado" ni "agrega").
- Minúscula al inicio, **sin punto final**, máximo **72 caracteres**.
- El **alcance** es el módulo o la pantalla tocada: `auth`, `pedidos`, `inventario`, `webhook`, `readme`. Una sola palabra, minúscula.

| Tipo | Cuándo |
|---|---|
| `feat` | Funcionalidad nueva visible para el usuario o la API |
| `fix` | Corrige un error |
| `refactor` | Cambia código sin cambiar comportamiento |
| `perf` | Mejora rendimiento |
| `style` | Formato, espacios, estilos visuales sin lógica |
| `docs` | Solo documentación |
| `test` | Agrega o corrige pruebas |
| `build` | Dependencias, empaquetado |
| `ci` | Pipelines (GitHub Actions, etc.) |
| `chore` | Mantenimiento que no encaja en lo anterior |

Buenos: `feat(pedidos): permitir dividir la cuenta por persona` · `fix(auth): rechazar tokens con algoritmo distinto a HS256` · `docs(readme): documentar variables de entorno`

Malos: `cambios`, `arreglos varios`, `WIP`, `Se actualizó el login.`, `fix: fix`

## 2. Un cambio lógico por commit

- Si el mensaje necesita "y" para describir dos cosas distintas, son dos commits.
- No mezclar refactor con fix: primero el refactor (sin cambio de comportamiento), luego el fix.
- Revisar `git diff --staged` antes de cada commit. Agregar archivos por nombre (`git add ruta`), no `git add -A` a ciegas.
- **Nunca** subir `.env`, credenciales, llaves, dumps de base de datos ni `node_modules`. Si pasa, rotar el secreto: borrarlo del historial no basta.

## 3. Ramas

Mismo prefijo que el tipo: `feat/dividir-cuenta`, `fix/token-expirado`, `docs/despliegue`, `refactor/servicio-pagos`. Minúsculas, guiones, corto.

- `main` (o `master`) siempre desplegable. **Nunca push directo a `main`**: todo entra por pull request.
- Si el repo usa `develop`, las ramas salen de `develop` y los releases son un PR `develop → main`.
- Una rama = un tema. Si el tema crece, partirla en PRs encadenados y decir en cada PR de cuál depende.

## 4. Pull requests

- **Título** con el mismo formato del commit: `feat(pedidos): permitir dividir la cuenta`.
- **Descripción**:
  ```
  ## Qué cambia
  - ...
  ## Por qué
  - ...
  ## Cómo se probó
  - comandos ejecutados y resultado (pruebas, build, prueba manual)
  ## Riesgos / pendientes
  - migraciones, variables de entorno nuevas, pasos de despliegue
  ```
- Antes de abrirlo: pruebas y build en verde en local. Después: revisar que el CI pase.
- Fusionar con un mensaje descriptivo (`Merge pull request #12 from usuario/feat/dividir-cuenta`) o squash con un título convencional; ser consistente dentro del repo.
- Borrar la rama al fusionar.

## 5. Releases y versiones

- Versionado semántico: `fix` → parche, `feat` → menor, `BREAKING CHANGE` → mayor.
- El CHANGELOG se arma agrupando los commits por tipo; por eso la primera línea tiene que ser clara.
- Etiquetas `vX.Y.Z` sobre `main` después del merge del release.

## 6. Corregir historial

- Mensaje mal escrito en el último commit **local**: `git commit --amend`.
- Commits locales desordenados: rebase antes de abrir el PR.
- **Nunca reescribir historial ya publicado** en ramas compartidas (`push --force` a `main`/`develop`). En una rama propia, solo `--force-with-lease`.

## Lista antes de cada commit

1. ¿Primera línea `tipo(alcance): descripción` en imperativo, ≤72, sin punto?
2. ¿Un solo cambio lógico?
3. ¿Revisé el diff staged? ¿Sin secretos ni archivos generados?
4. ¿Las pruebas pasan?
5. ¿Estoy en una rama `tipo/...` y no en `main`?
