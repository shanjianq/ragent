# Repository Guidelines

## Project Structure & Module Organization
- `bootstrap/`: Spring Boot application entrypoint (`RagentApplication`) and most business logic.
- `framework/`: shared infrastructure and common utilities used across modules.
- `infra-ai/`: model/provider integrations and AI infrastructure code.
- `mcp-server/`: MCP tool server module.
- `frontend/`: React + Vite admin/UI (TypeScript).
- `resources/`: shared assets and local infra configs (e.g., `resources/docker/milvus/`).
- `docs/`: architecture and examples; `scripts/`: ad-hoc shell scripts.
- Tests live under `bootstrap/src/test/java` (and follow the same package layout).

## Build, Test, and Development Commands
Backend (repo root):
- `./mvnw -pl bootstrap -am spring-boot:run` — run the API on `http://localhost:8080/api/ragent`.
- `./mvnw test` — run all backend tests across modules.
- `./mvnw -pl bootstrap -am package` — build backend artifacts.

Frontend (`frontend/`):
- `npm install` — install dependencies.
- `npm run dev` — Vite dev server (ports 5173+).
- `npm run build` — typecheck + production build.
- `npm run lint` / `npm run format` — ESLint + Prettier.

Infra (optional):
- `docker compose -f resources/docker/milvus/milvus-stack-2.6.6.compose.yaml up -d` — local Milvus stack.

## Coding Style & Naming Conventions
- Java 17, 4-space indentation; keep packages under `com.nageoffer.ai.ragent`.
- Spotless Maven plugin applies the license header from `resources/format/copyright.txt` during compile—avoid manual reformatting.
- Frontend uses Prettier (`tabWidth: 2`, `printWidth: 100`, semicolons) and ESLint. React components are PascalCase, hooks are `useX`, services end in `Service`.
- Test classes are named `*Tests` (see `bootstrap/src/test/java`).

## Testing Guidelines
- Backend tests use Spring Boot’s test starter (JUnit) and are runnable via `./mvnw test`.
- No automated frontend tests detected; follow the manual smoke steps in `frontend/TESTING.md`.

## Commit & Pull Request Guidelines
- Commit messages follow `type(scope): summary`, e.g. `feat(dashboard): ...`, `fix(prompt): ...`, `docs(readme): ...`, `refactor(...)`, `chore(...)`, `style(...)`, `optimize(...)`.
- PRs should include: a concise summary, testing performed, linked issues, and screenshots for UI changes. Call out any config/DB changes explicitly.

## Configuration & Security
- Runtime settings live in `bootstrap/src/main/resources/application.yaml` (MySQL, Redis, Milvus, model providers).
- Use env vars for secrets (e.g., `BAILIAN_API_KEY`, `SILICONFLOW_API_KEY`) and keep credentials out of commits.
