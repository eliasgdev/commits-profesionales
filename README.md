# Commits profesionales

Skill para **Claude Code** que aplica un flujo de git ordenado con **Conventional Commits en español**: formato de mensajes, un cambio lógico por commit, nombres de ramas, pull requests con descripción útil, merges y versionado semántico.

## Origen

Estas reglas salieron del trabajo diario en varios proyectos propios y de clientes, alojados en repositorios privados. Recogen las convenciones que terminé usando en todos ellos para que el historial se pueda leer y auditar. Las publico por si le sirven a alguien más.

## Qué cubre

- Formato `tipo(alcance): descripción` con la tabla de tipos y ejemplos buenos y malos.
- Cuándo partir un commit, qué revisar antes de cada uno y qué nunca subir.
- Ramas `feat/`, `fix/`, `docs/`… y el uso de `main` / `develop`.
- Plantilla de pull request (qué cambia, por qué, cómo se probó, riesgos).
- Releases, versionado semántico y cómo corregir historial sin romper nada.

## Instalación

```bash
git clone https://github.com/eliasgdev/commits-profesionales.git
mkdir -p ~/.claude/skills
cp -r commits-profesionales/commits-profesionales ~/.claude/skills/
```

Para un solo proyecto, cópiala en `.claude/skills/` dentro del repositorio. Claude Code la usa sola cuando vas a hacer un commit o abrir un PR.

## Licencia

MIT
