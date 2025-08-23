# Copilot Coding Agent Instructions

## Repository Overview
This repository contains the Docker Compose setup for Hoppscotch All-In-One (AIO) deployment. It is used to orchestrate the Hoppscotch stack using Docker containers.

## Coding Agent Best Practices

### 1. Preferred Languages & Tools
- **Primary language:** YAML (for Docker Compose)
- **Other tools:** Bash scripts, Markdown (for documentation)
- **Containerization:** Docker, Docker Compose

### 2. Code Style & Conventions
- Use clear, descriptive service names in `docker-compose.yml`.
- Use environment variables for configuration where possible.
- Keep comments concise and relevant.
- Follow [Docker Compose best practices](https://docs.docker.com/compose/best-practices/).

### 3. Pull Request & Commit Guidelines
- Each PR should address a single logical change.
- PRs must include a clear description of the change and its purpose.
- Reference related issues in PR descriptions when applicable.
- Use conventional commit messages (e.g., `feat:`, `fix:`, `docs:`).

### 4. Testing & Validation
- Validate Docker Compose files with `docker-compose config` before committing.
- Ensure all services start successfully with `docker-compose up`.
- Update documentation if configuration or usage changes.

### 5. Documentation
- Update `README.md` for any user-facing changes.
- Document new environment variables and configuration options.

### 6. Security
- Do not commit secrets or sensitive data.
- Use `.env` files for local development secrets (add to `.gitignore`).

### 7. Issue Management
- Use GitHub Issues for bug reports and feature requests.
- Tag issues appropriately (e.g., `bug`, `enhancement`).

---

For more information, see [Best practices for Copilot coding agent in your repository](https://gh.io/copilot-coding-agent-tips).
