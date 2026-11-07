# Estrategia Git y ramas — Aviario

> **Estado:** propuesta de trabajo. En la revisión del 8 de noviembre de 2026 no había rulesets activos en el repositorio. Las restricciones descritas aquí no se aplican automáticamente hasta que se configuren y activen en GitHub.

## Objetivo

Separar el trabajo diario de las versiones estables, facilitar contribuciones y mantener un historial recuperable sin añadir un proceso pesado a un proyecto que, de momento, tiene un único mantenedor.

## Ramas persistentes

| Rama | Función | Cómo recibe cambios |
| --- | --- | --- |
| `main` | Versión estable o publicable. No implica que exista ya una release. | PR desde `develop`, una vez validado |
| `develop` | Rama de integración; puede incluir funciones aún no publicadas. | PR desde ramas temporales |

## Ramas temporales

Usa el prefijo correspondiente y un nombre corto en minúsculas, por ejemplo `feature/login`.

- `feature/nombre`: nuevas funcionalidades (p. ej. `feature/login`).
- `fix/nombre`: corrección de errores (p. ej. `fix/login`).
- `docs/nombre`: documentación (p. ej. `docs/login`).
- `refactor/nombre`: mejoras internas sin cambiar el comportamiento (p. ej. `refactor/login`).
- `test/nombre`: pruebas automatizadas (p. ej. `test/login`).
- `chore/nombre`: mantenimiento y configuración (p. ej. `chore/login`).
- `hotfix/nombre`: correcciones urgentes de `main` (p. ej. `hotfix/login`). La rama parte de `main` y el cambio también se incorpora a `develop`.

No hace falta crearlas de antemano: abre una rama para cada cambio y elimínala después de fusionar el PR. El prefijo de rama `docs/` no es la carpeta `docs/` del repositorio.

## Flujo normal

```text
main (estable) ◄────────────── PR de publicación ◄──────── develop
                                                        ▲
                                                        │ PR
                                                   feature/login
                                                   docs/readme
                                                   fix/login
```

1. Sincroniza `develop`.
2. Crea una rama temporal desde `develop`.
3. Realiza cambios pequeños y commits claros.
4. Sube la rama (`push`) y abre un PR con base `develop`.
5. Revisa el diff, ejecuta pruebas y resuelve conversaciones.
6. Fusiona el PR y elimina la rama temporal.
7. Cuando `develop` esté listo, abre un PR `develop` → `main` y publica una versión si procede.

## Receta local: nuevo trabajo

```bash
git switch develop
git pull --ff-only origin develop
git switch -c docs/readme
# editar los archivos
git add .
git commit -m "docs: actualizar README"
git push -u origin docs/readme
```

Después abre GitHub y crea un pull request hacia `develop`.

## Actualizar la rama de trabajo

```bash
git fetch origin
git switch develop
git pull --ff-only origin develop
git switch feature/login
git merge develop
```

Resuelve cualquier conflicto y continúa. Este ejemplo presupone que la rama local `feature/login` ya existe. Si trabajas con un fork, ejecuta `git fetch upstream` y usa `git merge upstream/develop` en tu rama de trabajo.

## Políticas recomendadas (todavía no activadas)

Estas reglas describen el flujo deseado, **no el estado de protección actual**. Para aplicarlas, abre **Settings → Rules → Rulesets** en GitHub, crea o importa los rulesets y comprueba que estén activos.

- Bloquear borrados y `force push` en `main` y `develop`.
- Exigir pull requests para integrar cambios en esas ramas.
- Mientras haya un único mantenedor, usar **0 aprobaciones externas obligatorias**, aunque cada cambio se debe revisar antes de fusionarse.
- En `main`, requerir la resolución de conversaciones del PR; en `develop`, mantener flexibilidad al principio.
- No exigir pruebas CI hasta que haya comprobaciones automáticas configuradas y verificadas.
- Recomendar **Squash merge** para simplificar el historial, sin imponer todavía historial lineal.

Cuando se activen las reglas, prueba un PR real y comprueba su funcionamiento. Esta documentación por sí sola **no protege** ninguna rama.

## Nomenclatura de versiones

Cuando exista una primera entrega probada, se podrán usar versiones como `v0.1.0` y releases de GitHub. Un *tag* de Git no sirve para señalar que una rama está protegida ni reemplaza una release.

## Incidencias y aportaciones externas

- Ideas y errores → *Issues*.
- Implementaciones → *Pull requests* desde forks o ramas de colaboradores.
- Aceptar forks significa permitir que terceros desarrollen su copia, no permitir que escriban directamente en las ramas oficiales.
- La licencia Apache-2.0 permite redistribuir y modificar bajo sus condiciones; cualquier contribución debe ser legítima y compatible con dicha licencia.

Consulta [CONTRIBUTING.md](../CONTRIBUTING.md) para el procedimiento completo.
