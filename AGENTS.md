# Repository Guidelines

## Project Structure & Module Organization
Core code lives in `vfpy/`.
- `vfpy/devices/`: device-specific parsers and workflows (for example `hfa.py`).
- `vfpy/core/utils/`: shared helpers for OCR, image processing, and DICOM handling.
- `vfpy/core/dtypes/`: domain data structures used by scanners and outputs.
- `vfpy/core/errors/`: shared warnings and error types.

`README.md` contains usage examples and dependency notes. There is currently no committed `tests/` directory; new tests should be added under `tests/` and mirror the package layout.

## Build, Test, and Development Commands
This repository does not currently define a formal build system (`pyproject.toml`/`setup.py` is not present). Typical local setup:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install numpy pandas opencv-python wand pytesseract pydicom openpyxl xlsxwriter pytest
export PYTHONPATH=$PWD
```

Useful checks:
- `python -c "from vfpy.devices import hfa; print('import ok')"`: quick import smoke test.
- `python -m pytest -q`: run tests (once tests are added).

## Coding Style & Naming Conventions
Follow existing Python style in the repository:
- 4-space indentation, no tabs.
- `snake_case` for functions/variables, `PascalCase` for classes, `UPPER_CASE` for constants.
- Keep utility functions focused and side effects explicit (especially in OCR/image code paths).
- Use clear module names by responsibility (`ocrutils.py`, `dicomutils.py`, etc.).

## Testing Guidelines
Use `pytest` for new tests.
- Name files `test_<module>.py` and test functions `test_<behavior>()`.
- Add regression tests for OCR parsing, map extraction, and DICOM loading paths.
- Prefer small anonymized fixtures; never commit identifiable patient data.

## Commit & Pull Request Guidelines
Recent history uses short, single-line commit subjects (for example, `Update README.md`).
- Keep commit titles concise (about 50-72 chars) and action-oriented.
- Group related changes in one commit; avoid mixing refactors with behavior changes.
- PRs should include: purpose, affected modules, validation commands run, and sample output/screenshots for OCR-output changes.
- Link related issues and call out dependency/tooling changes clearly.

## Security & Configuration Tips
- Configure Tesseract explicitly via `set_path_to_tesseract(...)` before OCR runs.
- Ensure system tools (`tesseract`, `ghostscript`, `ImageMagick`) are installed locally.
- Treat DICOM inputs as sensitive; de-identify data before sharing in issues or PRs.
