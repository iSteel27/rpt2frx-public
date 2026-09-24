# rpt2frx 0.1.0-beta.1 (pre-release)

First public beta. Converts Crystal Reports (.rpt) into FastReport templates (.frx).

**Requires** Windows 10/11 64-bit and the free 64-bit SAP Crystal Reports runtime (installed separately from SAP; the installer checks for it).

## Install
Download `rpt2frxSetup-0.1.0-beta.1.exe`, run it, and open a new terminal. The installer is not code-signed, so Windows may show "unknown publisher": choose **More info > Run anyway**.

## Quick start
```
rpt2frx doctor
rpt2frx "C:\Reports\Sales.rpt" --preview
```

## Verify the download
SHA-256: `9FA8FC2BDF8952DFC3384F179DA4C033FA7F1EBA01298FA7DAE9525B7DA36D04`
(`Get-FileHash rpt2frxSetup-0.1.0-beta.1.exe` in PowerShell)

## New
- `rpt2frx` command (added to PATH by the installer), `--version`, `--help`
- `rpt2frx file.rpt` writes a `.frx` directly; `--preview` renders sample pages
- Setup check (`rpt2frx doctor`) and installer system-check page
- Table borders that span group header and detail rows now convert correctly; near-horizontal lines are no longer drawn slanted

## Known issues
- Logos are not exported (use `--picture`); some formula functions, subreports, charts and cross-tabs are not converted (reported as warnings)
- Installer is unsigned
