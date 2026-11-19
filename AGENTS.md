# Report and presentation formatting

- Keep report references or bibliography on a page by itself by default.
- Keep presentation references on a dedicated final slide by default.
- Use a different layout only when the user or task prompt explicitly requests it.

## Project references

- Primary report: [Group-2-Report.tex](<./MAIN SLOP/Group-2-Report.tex>)
- Primary presentation: [Group-2-Presentation.tex](<./MAIN SLOP/Group-2-Presentation.tex>)
- Report and presentation bibliography: [citations.bib](<./MAIN SLOP/citations.bib>)
- Group report template: [Group-X-Report.tex](<./Base Template/Group-X-Report.tex>)
- Group project instructions: [Group Project Instructions.pdf](<./Base Template/Group Project Instructions.pdf>)

## Building the primary report

After every update to the primary report or its bibliography, rebuild the PDF before finishing. Run these PowerShell commands from the repository root; the generated PDF is `MAIN SLOP/Group-2-Report.pdf`:

```powershell
Push-Location "MAIN SLOP"
try {
    pdflatex -interaction=nonstopmode -halt-on-error "Group-2-Report.tex"
    if ($LASTEXITCODE -ne 0) { throw "pdflatex failed on the first pass." }
    bibtex "Group-2-Report"
    if ($LASTEXITCODE -ne 0) { throw "bibtex failed." }
    pdflatex -interaction=nonstopmode -halt-on-error "Group-2-Report.tex"
    if ($LASTEXITCODE -ne 0) { throw "pdflatex failed on the second pass." }
    pdflatex -interaction=nonstopmode -halt-on-error "Group-2-Report.tex"
    if ($LASTEXITCODE -ne 0) { throw "pdflatex failed on the final pass." }
} finally {
    Pop-Location
}
```

## Building the primary presentation

After every update to the primary presentation or its bibliography, rebuild the PDF before finishing. Run these PowerShell commands from the repository root; the generated PDF is `MAIN SLOP/Group-2-Presentation.pdf`:

```powershell
Push-Location "MAIN SLOP"
try {
    pdflatex -interaction=nonstopmode -halt-on-error "Group-2-Presentation.tex"
    if ($LASTEXITCODE -ne 0) { throw "pdflatex failed on the first pass." }
    bibtex "Group-2-Presentation"
    if ($LASTEXITCODE -ne 0) { throw "bibtex failed." }
    pdflatex -interaction=nonstopmode -halt-on-error "Group-2-Presentation.tex"
    if ($LASTEXITCODE -ne 0) { throw "pdflatex failed on the second pass." }
    pdflatex -interaction=nonstopmode -halt-on-error "Group-2-Presentation.tex"
    if ($LASTEXITCODE -ne 0) { throw "pdflatex failed on the final pass." }
} finally {
    Pop-Location
}
```
