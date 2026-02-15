# Changelog

All notable changes to this repository are documented in this file.

## [Unreleased]

### Added
- Added `AGENTS.md` contributor guide (`Repository Guidelines`) with project structure, setup commands, coding/testing conventions, and OCR data-handling notes.
- Added `.gitignore` for Python bytecode, caches, virtual environments, IDE files, and local output artifacts.

### Changed
- Added optional non-GUI processing path (`process(show_process=False)`) and propagated `show_process` through OCR/ROI calls.
- Updated `from_pdf(...)` to support TIFF input directly and load grayscale image data.
- Added protocol detection fallback (`10-2`, `24-2`, `30-2`, `60-4`) and safe behavior when protocol cannot be detected.
- Improved robustness of line/landmark splitting and top/bottom bar detection.
- Made map reshaping and conversion logic defensive when ROI counts do not match hardcoded assumptions.
- Hardened `save(...)` to tolerate missing/redacted fields (name/date/eye) and partial outputs.

### Fixed
- NumPy 2.x compatibility by replacing removed aliases (`np.float`, `np.bool`, `np.NaN`) with supported types/usages.
- Headless/WSL compatibility by adding safe `tkinter` fallback, guarding image utilities against empty crops/contours, and updating Excel writer usage.

### Verified
- Confirmed end-to-end run on:
  - `/mnt/c/Users/Thierry/Documents/Hong_Eyes/VF_OD_2023-12-11.tiff`
  - Environment: `~/.venvVFPy` + Ubuntu `tesseract` binary (`/usr/bin/tesseract`)
- Output artifacts generated under:
  - `/tmp/vfpy_output/UnknownSubject_UnknownDate_Right_OCROutput`

### Known Limitations
- True HFA-2 parsing (especially `24-2`) is not yet fully implemented; current run uses temporary `60-4` heuristics fallback to avoid hard failure.
- Redacted fields (e.g., name/DoB) reduce scan parameter completeness.

## [2026-02-15] - Initial Modernization Baseline

### Added
- Baseline contributor and change-tracking documentation.

### Changed
- Initial runtime modernization for current Python/NumPy ecosystem and WSL execution.

### Notes
- Established a working baseline for TIFF processing while full HFA-2 (`24-2`) support remains pending.
