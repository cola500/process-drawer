---
title: Process Drawer
description: Minimal drag-och-släpp processritare i en HTML-fil. Noll dependencies.
category: tool
status: live
last_updated: 2026-04-19
sections: [Vad är det, Funktioner, Använd den, Hur det byggdes, Teknik]
---

# Process Drawer

En enkel processritare för att rita organisationsprocesser. Drag-och-släpp boxar, koppla med pilar, lägg till etiketter, exportera till SVG. Allt sparas automatiskt i webbläsaren.

**Live demo:** https://cola500.github.io/process-drawer/

## Vad är det

Ett minimalt verktyg för att dokumentera processer — typ som en digital whiteboard med stöd för BPMN-liknande former (process, beslut, start/slut). Byggt för att vara så enkelt som möjligt att använda och läsa.

Hela appen är **en HTML-fil** med inline JS och CSS. Inga bibliotek, ingen build-process, ingen backend.

## Funktioner

- **3 shape-typer**: Process (rektangel), Beslut (romb), Start/Slut (oval)
- **2 pil-typer**: Solid eller streckad (klicka pilen för att växla)
- **Pil-etiketter**: Dubbelklick på pil för att lägga till t.ex. "Ja" / "Nej"
- **Redigera text**: Dubbelklick på en box för att byta namn
- **Ta bort**: Hover över box eller pil → ✕-knapp
- **Auto-save**: Allt sparas i `localStorage` vid varje förändring
- **JSON-import/export**: Spara till fil, ladda från fil, dela med andra
- **SVG-export**: Ladda ner ditt diagram som .svg (öppnas i webbläsare/Figma/etc)

## Använd den

1. Öppna https://cola500.github.io/process-drawer/
2. Klicka på en shape-knapp för att lägga till en box
3. Dra boxar för att placera dem
4. Klicka två boxar i följd för att koppla dem med pil
5. Dubbelklick för att redigera (text på boxar, etikett på pilar)
6. Exportera till SVG eller JSON när du är klar

## Hur det byggdes

Byggt iterativt i 5 steg via Claude Code, totalt ca 30 minuters implementationstid:

1. **Drag-drop boxar + pilar** — kärnfunktionen
2. **Shape-typer + pil-typer** — uttrycksfullhet
3. **Edit + delete** — från demo till användbart
4. **Pil-etiketter + SVG-export** — polish + sharing
5. **Persistens** — auto-save + JSON I/O

Varje iteration startade med en hypotes ("kan användaren X på under Y sekunder?"), byggde minsta möjliga, och verifierades manuellt innan nästa.

## Teknik

- **Vanilla JavaScript** (ingen framework)
- **SVG** för pilar och pil-etiketter
- **HTML/CSS** för boxar och layout
- **localStorage** för persistens
- **En fil**, ca 400 rader

## Licens

MIT
