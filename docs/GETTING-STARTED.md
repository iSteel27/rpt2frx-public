# rpt2frx — Getting started (beta)

rpt2frx converts Crystal Reports (`.rpt`) into FastReport templates (`.frx`). It reads only the report *design*; no data is read and **nothing is uploaded anywhere** — everything runs on your PC.

## 1. What you need
| Requirement | How to check |
|---|---|
| Windows 10/11, 64-bit | — |
| .NET Framework 4.8 (built into Windows 10 May 2019+ / 11) | `rpt2frx doctor` |
| **SAP Crystal Reports runtime, 64-bit** (free from SAP, *not* bundled) | `rpt2frx doctor` |

The installer checks these for you and gives download buttons if something is missing.

## 2. Install
1. Download `rpt2frxSetup-<version>.exe` from the link you were sent.
2. Run it. Windows may say "unknown publisher" during the beta: choose **More info → Run anyway**.
3. Keep **Add rpt2frx to PATH** ticked, then finish. Open a **new** terminal window afterwards.

## 3. Your first conversion
```
rpt2frx --version
rpt2frx doctor
rpt2frx "C:\Reports\Sales.rpt"
```
This writes `Sales.frx` next to the report. Add `--preview` to also get `Sales.preview.pdf` and `.png` images (filled with *sample* data) so you can check the layout.

Other ways: right-click a `.rpt` → **Convert with rpt2frx**; or run `rpt2frx` with no arguments for a guided menu.

## 4. Opening the result
- Quick look: use `--preview` and open the PDF/PNG.
- Real editing: open the `.frx` in **FastReport Community Designer** (free, from the FastReport open-source project) and connect your own data source.

## 5. Useful options
| Option | Meaning |
|---|---|
| `--preview` | render sample pages next to the `.frx` |
| `--font-scale 0.87` | match Crystal's text width (default in shortcut mode) |
| `--picture logo.png` | use this image for logos (Crystal does not expose image bytes) |
| `--out file.frx` | choose the output name |
| `extract --in x.rpt` | write the JSON metadata only |

## 6. Troubleshooting
| Symptom | Cause / fix |
|---|---|
| `'rpt2frx' is not recognized` | Open a **new** terminal; or re-run the installer with "Add to PATH" ticked |
| doctor: SAP runtime FAIL | Install the **64-bit** runtime (`CRRuntime_64bit_13_0_xx.msi`) from SAP, then re-run `rpt2frx doctor` |
| doctor: .NET Framework 4.8 FAIL | Run Windows Update or install .NET Framework 4.8 from Microsoft |
| Extractor "does not start" / code -532462766 | Files incomplete: close all rpt2frx windows and reinstall |
| Report "cannot be loaded" | File is not a valid/complete `.rpt` or is password protected |
| Warnings listed after conversion | Items needing manual attention (unsupported formulas etc.) — see Known limits |

## 7. Known limits (beta)
- Logo/picture bytes are not exported; use `--picture`.
- Some Crystal functions (`propercase`, `towords`, `left` …) and `Sum(...)` suppress conditions are not translated; a warning is printed.
- Subreports and complex formulas may need hand-tuning; layout is close but not pixel-identical.

## 8. Reporting a problem
Run `rpt2frx doctor`, copy its output, attach the newest file from `%LOCALAPPDATA%\CrystalMetadata\logs`, and describe what you expected. **Do not send reports containing confidential information** — a screenshot of the layout with data hidden is enough.
