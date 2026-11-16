# Report formatting

- Keep the references or bibliography on a page by itself by default.
- Use a different layout only when the user or task prompt explicitly requests it.

## Project references

- Current main report: [Copilot Report.tex](<./Copilot Slop/Copilot Report.tex>)
- Group X report template: [Group-X-Report.tex](<./Base Template/Group-X-Report.tex>)
- Group project instructions: [Group Project Instructions.pdf](<./Base Template/Group Project Instructions.pdf>)

## Building the main report

After every update to the main report or its bibliography, rebuild the PDF before finishing. Run these PowerShell commands from the repository root; the generated PDF is `Copilot Slop/Copilot Report.pdf`:

```powershell
Push-Location "Copilot Slop"
try {
    pdflatex -interaction=nonstopmode -halt-on-error "Copilot Report.tex"
    if ($LASTEXITCODE -ne 0) { throw "pdflatex failed on the first pass." }
    bibtex "Copilot Report"
    if ($LASTEXITCODE -ne 0) { throw "bibtex failed." }
    pdflatex -interaction=nonstopmode -halt-on-error "Copilot Report.tex"
    if ($LASTEXITCODE -ne 0) { throw "pdflatex failed on the second pass." }
    pdflatex -interaction=nonstopmode -halt-on-error "Copilot Report.tex"
    if ($LASTEXITCODE -ne 0) { throw "pdflatex failed on the final pass." }
} finally {
    Pop-Location
}
```
