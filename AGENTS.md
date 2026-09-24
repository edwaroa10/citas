# AGENTS.md — Orquestación del workspace `citas`

## Alcance y fuentes de verdad

Este archivo coordina `citas-api` y `citas-web`; no implementa funcionalidades por sí mismo.

Orden de evidencia: `PRD.md`, `RESTRICCIONES_TECNICAS.md`, `database/REQUISITOS_NORMALIZACION_3FN.md`, HU/CA/DoD aprobados, contratos y decisiones de la LLM Wiki, y finalmente código/pruebas/diseño aprobado.

No inventar requisitos ni resolver ambigüedades funcionales por inferencia.

## Límites de repositorio

- `citas-api`: dominio, casos de uso, adaptadores REST/persistencia, seguridad, Flyway, pruebas backend, contratos y n8n.
- `citas-web`: UI TypeScript, integración REST directa, accesibilidad, estados de interfaz, build y pruebas frontend.
- No usar Express ni BFF.
- No editar ambos repositorios salvo cambios explícitamente cross-repo.

Los `AGENTS.md` específicos prevalecen dentro de su repositorio cuando existan.

## Flujo de trabajo

1. Identificar HU, CA y DoD aprobados.
2. Clasificar el cambio como backend, frontend o cross-repo.
3. Antes de un cambio cross-repo, enumerar repositorios, archivos, contrato, pruebas y evidencia.
4. Implementar en `develop`, validar y documentar evidencia.
5. Mantener `main` estable y no reescribir historial.

## Contratos REST

Un cambio de contrato requiere documentación en la wiki, evidencia backend (endpoint, validación y pruebas), evidencia frontend (cliente, estados y build/typecheck/pruebas) y una decisión de compatibilidad o versionado.

## Datos y secretos

Usar únicamente datos sintéticos, salvo sedes o datos públicos incluidos expresamente en requisitos. No abrir, mostrar ni versionar secretos, tokens, credenciales o contenido de `.env`; nunca registrar passwords, tokens o PII innecesaria.

## LLM Wiki global

La única wiki vive en `citas-api/docs/wiki/llm-wiki/`:

- `raw/`: fuentes curadas e inmutables y sus registros de procedencia.
- `wiki/`: conocimiento verificable y enlazado.
- `schema/`: convenciones operativas.
- Leer `wiki/index.md` antes de consultar o modificar la wiki.
- `wiki/log.md` es append-only para INGEST, QUERY, LEARN y LINT.
- No guardar transcripciones, secretos, PII ni contenido privado real.

## Automatizaciones y diseño

- Los workflows n8n se versionan como JSON en `citas-api/automations/n8n/` y nunca incluyen credenciales.
- `scrum-spec-orchestrator` solo escribe en `citas-api/docs/wiki/scrum/` y no implementa código.
- Stitch/AI Studio gobierna la fuente visual del frontend; no define backend.
