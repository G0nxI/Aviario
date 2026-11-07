# Contribuir a Aviario

¡Gracias por querer colaborar! Aviario es un proyecto abierto que comienza por la gestión de jaulas y crecerá hacia la gestión de aves, especies, cría, genealogía y cuidados. Se aceptan sugerencias, documentación, pruebas, correcciones y nuevas funcionalidades.

> **Estado actual:** proyecto en desarrollo inicial; el código, las APIs y la estructura pueden cambiar. Antes de desarrollar una funcionalidad grande, abre un *issue* para hablar sobre el alcance.

## 1. Formas de participar

- **Ideas y necesidades:** abre un *issue* de propuesta, explicando el problema que quieres resolver.
- **Errores:** abre un *issue* con pasos para reproducir el fallo, resultado esperado y observado; evita publicar datos personales o credenciales.
- **Documentación y pruebas:** son contribuciones tan útiles como el código.
- **Código:** realiza un *fork* y abre un *pull request* (PR). No necesitas permisos de escritura sobre el repositorio original.

## 2. Antes de empezar

1. Comprueba que no existe ya un *issue* o PR similar.
2. Para cambios de alcance significativo, comenta primero la idea en un *issue*.
3. Mantén las propuestas acotadas: un PR debería resolver un problema concreto.
4. Respeta la licencia [Apache-2.0](LICENSE) del proyecto y las licencias de sus dependencias.

## 3. Flujo de trabajo con Git

**Repositorio con permisos de escritura:**

```bash
git clone https://github.com/G0nxI/Aviario.git
cd Aviario
git switch develop
git pull --ff-only origin develop
git switch -c feature/nombre-breve
```

**Si participas mediante fork:** crea un fork desde GitHub, clónalo y mantén el repositorio original como `upstream`. Asegúrate de partir de `upstream/develop`:

```bash
git clone https://github.com/TU_USUARIO/Aviario.git
cd Aviario
git remote add upstream https://github.com/G0nxI/Aviario.git
git fetch upstream
git switch -c feature/nombre-breve upstream/develop
```

Cuando termines:

```bash
git status
git add .
git commit -m "feat(jaulas): añadir validación de capacidad"
git push -u origin feature/nombre-breve
```

Abre un PR **hacia `G0nxI/Aviario:develop`**. Indica qué cambia, cómo se ha comprobado y, si existe, a qué *issue* corresponde. No abras PR directamente contra `main`, salvo una corrección urgente acordada con el mantenedor. En ese caso, la rama `hotfix/*` parte de `main` y el cambio debe trasladarse también a `develop`.

## 4. Convenciones

| Tipo | Ejemplo | Uso |
| --- | --- | --- |
| `feature/` | `feature/jaulas` | Nueva función |
| `fix/` | `fix/login` | Corrección |
| `docs/` | `docs/arquitectura` | Documentación |
| `refactor/` | `refactor/jaula-modelo` | Cambios internos sin alterar comportamiento |
| `test/` | `test/jaulas-api` | Pruebas |
| `chore/` | `chore/docker` | Mantenimiento |
| `hotfix/` | `hotfix/login` | Incidencia urgente sobre la versión estable (`main`); integrar la corrección también en `develop` |

Mensajes de commit recomendados (todavía no exigidos por un ruleset): `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`. Ejemplo: `docs: explicar el flujo de ramas`.

## 5. Calidad y seguridad

- Cuando se publique el código, sigue la arquitectura documentada y evita mezclar presentación, reglas de negocio y acceso a datos sin justificación.
- Incluye las pruebas o verificaciones que correspondan al cambio; explica lo que no hayas podido comprobar.
- No subas `.env`, contraseñas, tokens, copias reales de bases de datos ni datos de usuarios.
- Documenta los nuevos endpoints y los cambios de esquema.
- No rompas deliberadamente la compatibilidad sin comunicarlo previamente.
- Un PR puede requerir cambios o no ser aceptado si no encaja con el alcance del proyecto.

## 6. Revisión e integración

Los PR se integran en `develop` una vez revisados y probados. `main` recibe versiones consideradas estables a través de un PR desde `develop`. El mantenedor del proyecto decide qué se integra y cuándo; crear un fork no implica que las aportaciones se incorporen automáticamente.

Para más detalles, consulta [Flujo de ramas](docs/GIT_Y_RAMAS.md).
