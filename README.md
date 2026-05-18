# github_actions_demo

Laboratorio de CI/CD con GitHub Actions y Python.

## Estructura

```
github_actions_demo/
├── .github/
│   └── workflows/
│       └── devops.yml          # Workflow principal de CI/CD
├── hello.py                    # Aplicación Python simple
├── tests/
│   └── test_hello.py           # Tests unitarios
├── requirements.txt            # Dependencias Python
└── README.md                   # Documentación del proyecto
```

## Uso local

```bash
python -m pip install -r requirements.txt
export PYTHONPATH="${PYTHONPATH}:$(pwd)"
pytest -q
```

## Pipeline

El workflow `devops.yml` ejecuta los jobs:

1. **test** — instala dependencias, corre `pytest` y publica un `build_tag` como output.
2. **package** — depende de `test`, empaqueta `hello.py` en un `.zip` etiquetado con el `build_tag`.
3. **docs** — depende de `test` y `package`, imprime metadatos del repo y del runner.
4. **deploy** — depende de `docs`, simula el despliegue (solo se ejecuta en `main`).

## Flujo de trabajo

- Trabajo basado en ramas de feature (`feature/*`).
- Commits siguiendo [Conventional Commits](https://www.conventionalcommits.org/).
- Pull Requests a `main` con revisión y aprobación obligatoria.
