# Process Drawer

> En processritare i en HTML-fil. Noll dependencies, noll build, noll backend. Klistra in i en mapp eller öppna live.

🔗 **Live:** [cola500.github.io/process-drawer](https://cola500.github.io/process-drawer/)

<!-- TODO: lägg in en screenshot av verktyget med en exempel-process
     (5-6 boxar, ett beslut, "Ja"/"Nej"-pilar). Tag den direkt från
     live-demon, exportera som SVG, screenshota. -->

Ibland behöver man rita en process snabbt — i ett möte, för en kollega, i ett retro — och man vill inte starta Miro, Lucid eller en Figma-fil. Det här verktyget öppnar man, ritar i, exporterar SVG och stänger. Allt sparas automatiskt i webbläsaren.

Hela appen är **en HTML-fil** med inline JS och CSS. Det är medvetet det. Inga frameworks, inga build-steg, ingen leverantörsupplåsning.

## Vad detta repo visar

- **"Hur lite räcker?"-disciplin** — verktyget hade kunnat byggas i React med Tailwind med Tauri-wrapper. Det blev en HTML-fil. Beslutet är värt mer än koden.
- **Vertikala slices i sju steg** — README beskriver hur det byggdes iterativt, en hypotes per slice ("kan användaren X på under Y sekunder?"). Bygg → verifiera → nästa.
- **Pointer Events från start** — fungerar likvärdigt med mus och touch, utan branching. Liten teknisk detalj, stor signal om hantverk.
- **Auto-save + JSON I/O + SVG-export** — användarsäker design med små medel.

Byggt för egen del när inget annat verktyg kändes lagom — och kvar för att det fortfarande är det.

---

## Vad är det

Ett minimalt verktyg för att dokumentera processer — typ som en digital whiteboard med stöd för BPMN-liknande former (process, beslut, start/slut). Byggt för att vara så enkelt som möjligt att använda och läsa.

Hela appen är **en HTML-fil** med inline JS och CSS. Inga bibliotek, ingen build-process, ingen backend.

## Funktioner

- **3 shape-typer**: Process (rektangel), Beslut (romb), Start/Slut (oval)
- **2 pil-typer**: Solid eller streckad (klicka/tappa pilen för att växla)
- **Pil-etiketter**: Dubbelklick/dubbeltap på pil för att lägga till t.ex. "Ja" / "Nej"
- **Redigera text**: Dubbelklick/dubbeltap på en box för att byta namn
- **Ta bort**: ✕-knapp på box eller pil (syns alltid på touch, vid hover på desktop)
- **Auto-save**: Allt sparas i `localStorage` vid varje förändring
- **JSON-import/export**: Spara till fil, ladda från fil, dela med andra
- **SVG-export**: Ladda ner ditt diagram som .svg (öppnas i webbläsare/Figma/etc)
- **Pan**: Dra på bakgrunden för att flytta hela kartan (sparas också)
- **Mobil + desktop**: Pointer Events under huven, fungerar likvärdigt med mus och touch

## Använd den

1. Öppna https://cola500.github.io/process-drawer/
2. Klicka på en shape-knapp för att lägga till en box
3. Dra boxar för att placera dem
4. Klicka två boxar i följd för att koppla dem med pil
5. Dubbelklick för att redigera (text på boxar, etikett på pilar)
6. Exportera till SVG eller JSON när du är klar

## Hur det byggdes

Byggt iterativt i 7 steg via Claude Code:

1. **Drag-drop boxar + pilar** — kärnfunktionen
2. **Shape-typer + pil-typer** — uttrycksfullhet
3. **Edit + delete** — från demo till användbart
4. **Pil-etiketter + SVG-export** — polish + sharing
5. **Persistens** — auto-save + JSON I/O
6. **Mobilstöd** — Pointer Events, touch-targets, dubbeltap
7. **Pan på canvas** — dra bakgrunden för att flytta hela kartan

Varje iteration startade med en hypotes ("kan användaren X på under Y sekunder?"), byggde minsta möjliga, och verifierades manuellt innan nästa.

## Teknik

- **Vanilla JavaScript** (ingen framework)
- **SVG** för pilar och pil-etiketter
- **HTML/CSS** för boxar och layout
- **localStorage** för persistens
- **En fil**, ca 400 rader

## Licens

MIT
