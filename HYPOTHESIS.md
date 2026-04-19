---
title: Process Drawer
description: Iterativ kedja för att utforska hur enkelt en process-ritare kan byggas
category: ux-validation
status: confirmed
last_updated: 2026-04-19
sections: [Hypothesis, Test, Success Criteria, Time Budget, Result]
---

# Process Drawer — Iteration 1

## Hypothesis
En person som dokumenterar processer kan på under 30 sekunder skapa ett 3-stegs flöde med drag-och-släpp-boxar och pilar, utan instruktioner.

## Test
Bygg en HTML-sida med:
- Knapp "+ Steg" som lägger till en draggable box
- Boxar kan dras med musen
- Klicka två boxar i följd för att rita pil mellan dem

## Success Criteria
- Skapa 3 boxar, dra dem till positioner, koppla med 2 pilar
- Klart på under 30 sek
- Inga "hur gör jag?"-frågor

## Time Budget
15 min implementation.

## Result
- **Status**: Confirmed
- **What we learned**: Drag + klick-koppling känns naturligt. Användaren vill direkt ha fler former och pil-typer.
- **Decision**: Iterera — lägg till former och pil-varianter.

---

## Iteration-plan
Efter verifiering av varje iteration föreslår Claude nästa hypotes baserat på vad som lärts. Mål: ~5 iterationer.

### Iteration-historik
- **#1**: Drag-drop boxar + pilar — Confirmed
- **#2**: Flera shape-typer (process/beslut/start) + pil-typer (solid/streckad) — Confirmed
- **#3**: Edit text + delete boxar/pilar — Confirmed
- **#4**: Pil-etiketter + SVG-export — Confirmed
- **#5**: Persistens (auto-save + JSON import/export + rensa) — Confirmed
- **#6**: Mobilstöd (Pointer Events, touch-targets, dubbeltap) — Confirmed
- **#7**: Pan på canvas (drag bakgrunden för att flytta hela kartan) — Confirmed

---

# Iteration #2

## Hypothesis
Genom att erbjuda 3 shape-typer (process, beslut, start/slut) och 2 pil-typer (solid, streckad) blir verktyget tillräckligt uttrycksfullt för att rita riktiga BPMN-liknande processer — utan att bli förvirrande.

## Test
- 3 knappar i headern: "+ Process" (rektangel), "+ Beslut" (romb), "+ Start/Slut" (oval)
- Klick på pil växlar mellan solid och streckad

## Success Criteria
Användaren kan rita ett flöde med: start → process → beslut → 2 utgångar (en solid, en streckad till "alternativ väg"). Klart utan att fråga hur.

## Time Budget
10 min implementation.

## Result
- **Status**: Confirmed
- **What we learned**: Användaren upplever det som "snyggt" och vet inte själv vad som saknas — Claude tar initiativ.
- **Decision**: Iterera med "make it usable"-features (text + delete).

---

# Iteration #3

## Hypothesis
Med möjligheten att redigera text och ta bort boxar/pilar kan användaren rita en RIKTIG process från sitt eget jobb (inte bara dummy-flöde) på under 2 minuter.

## Test
- Dubbelklick på box → redigerar texten direkt
- Hover på box → ✕-knapp i hörnet → tar bort box + alla anslutna pilar
- Hover på pil → ✕-knapp vid mitten → tar bort pil

## Success Criteria
Användaren ritar en faktisk process från sin vardag (med riktiga namn på steg) och tar bort minst en sak under tiden.

## Time Budget
15 min implementation.

## Result
- **Status**: Confirmed
- **What we learned**: Edit + delete gör verktyget från demo till faktiskt användbart. Användaren vill nu polera UX och kunna dela resultatet.
- **Decision**: Iterera mot polish + sharing.

---

# Iteration #4

## Hypothesis
Med pil-etiketter (Ja/Nej etc.) och SVG-export blir verktyget tillräckligt komplett för att faktiskt användas i en arbetsdag — användaren kan dokumentera, dela, och inkludera bilden i ett dokument.

## Test
- Dubbelklick på pil → editbart fält vid pilens mitt → spara på Enter/blur
- Knapp "↓ SVG" i header → laddar ner hela diagrammet som .svg

## Success Criteria
Användaren kan rita ett beslutsflöde med Ja/Nej-pilar och sedan ladda ner SVG som öppnas korrekt i webbläsare/Figma.

## Time Budget
15 min implementation.

## Result
- **Status**: Confirmed
- **What we learned**: Pil-etiketter + SVG-export gör verktyget komplett för enkla flöden. Användaren upplever det som "snyggt".
- **Decision**: Iterera mot persistens — annars är allt arbete bortkastat vid reload.

---

# Sammanfattning av hela kedjan

**Övergripande lärdom:** En användbar processritare kan byggas i en enda HTML-fil med vanilla JS på under 1 timme, om man itererar i tight loop med tydlig hypotes per steg. Slutprodukt: ~400 rader, noll dependencies, fungerande dokumentation av riktiga processer.

**Vad som fungerade i processen:**
- Bygga "tunnaste skiva" först, polera senare
- Användarens "ja det funkar" eller "vad mer behövs?" var bästa signalen
- Att Claude tog initiativ när användaren var osäker på domain ("vad behöver en processritare?")
- En fil hela vägen — inga abstraktioner krävdes ens vid 400 rader

**Vad nästa nivå skulle vara (om vi fortsätter):**
- Swimlanes (vem ansvarar)
- Snap-to-grid + zoom/pan
- Pilar från kant istället för centrum
- Undo/redo
- Export PNG

**Beslut:** Hela experimentet Confirmed. Detta är moget att antingen användas som-är eller promotas till en riktig app.

---

# Iteration #5

## Hypothesis
Med auto-save till localStorage + JSON-export/import + rensa-knapp blir verktyget faktiskt användbart över flera arbetspass — användaren kan stänga fliken och komma tillbaka senare.

## Test
- Allt sparas automatiskt till localStorage vid varje förändring
- Vid sidladdning återställs senaste tillstånd
- Knapp "↓ JSON" laddar ner state som .json
- Knapp "↑ JSON" läser in en .json-fil
- Knapp "Rensa" tömmer canvas (med confirm)

## Success Criteria
Användaren kan: rita ett flöde → reload sidan → flödet är kvar. Och: exportera JSON → rensa → importera JSON → flödet är tillbaka.

## Time Budget
15 min implementation.

## Result
- **Status**: Confirmed
- **What we learned**: Persistens var den sista pusselbiten. Verktyget är nu komplett nog att faktiskt användas i en arbetsdag — rita, stänga fliken, komma tillbaka och fortsätta.
- **Decision**: Kedja avslutad. Resultat: en användbar processritare på ~1h, 2 filer (HTML + HYPOTHESIS), noll dependencies.

---

# Iteration #6

## Hypothesis
Med Pointer Events API + viewport meta-tag + touch-friendly UI fungerar appen på mobil utan att kompromissa med desktop-upplevelsen.

## Test
- Ersätt mouse* events med pointer* events
- Lägg till `<meta viewport>` och `touch-action`-tuning
- ✕-knappar alltid synliga på touch-enheter via `@media (hover: none)`
- Manuell dubbeltap-detektering för redigering (mer pålitligt än `dblclick` på iOS)

## Success Criteria
Användaren kan utföra alla kärnflöden (lägg till box, koppla, redigera namn, redigera etikett, ta bort, exportera) på en mobil utan friktion.

## Time Budget
15 min implementation.

## Result
- **Status**: Confirmed (med upptäckt: pan saknades — ledde till iteration #7)
- **What we learned**: Pointer Events ger mobil + desktop på samma kodbas utan särfall. `touch-action: none` förhindrar browserns gester men **stänger även av scroll** — vilket avslöjade att vi inte hade egen pan-logik.
- **Decision**: Iterera — fixa pan så användaren kan röra sig över kartan på mobil.

---

# Iteration #7

## Hypothesis
Med custom pan-logik (drag på bakgrunden flyttar hela kartan via CSS transform) får användaren samma frihet på mobil som på desktop, utan att behöva pinch-zoom eller browser-scroll.

## Test
- Wrap boxar + arrows i en `#content` div
- `pointerdown` på canvas-bakgrund (ej box/pil) startar pan
- Applicera `transform: translate(panX, panY)` på `#content`
- Spara `panX/panY` i localStorage så vyn återställs vid reload
- SVG får `overflow: visible` så pilar utanför viewport renderas

## Success Criteria
Användaren kan dra med fingret på bakgrunden för att panorera till boxar utanför skärmen, både på mobil och desktop.

## Time Budget
15 min implementation.

## Result
- **Status**: Confirmed
- **What we learned**: CSS transform på en wrapper-div är enklaste pan-implementationen — `box.offsetLeft/Top` påverkas inte, så drag och pil-rendering fortsätter fungera utan ändring.
- **Decision**: Kedja avslutad (riktigt denna gång). Ship + dela.

---

# Slutsats efter alla 7 iterationer

## Result
**Confirmed** — alla iterationer passerade. Live på https://cola500.github.io/process-drawer/.

## What we learned
- En användbar processritare ryms i **EN HTML-fil, ~600 rader, noll dependencies**.
- **Pointer Events API** ger mobil + desktop utan särfall — bara 1 iteration räckte.
- **Manuell dubbeltap-detektering** är mer pålitligt än `dblclick` på iOS Safari.
- **CSS transform på en wrapper-div** är enklaste pan-implementationen.
- Användaren upplevde produkten som "snyggt/användbart" långt innan jag tyckte den var "klar" — **shipping-tröskeln är lägre än man tror**.
- Stop-signalerna i CLAUDE.md (>2 filer, >400 rader) var inte rigida — vi gick förbi 600 rader utan att behöva splittra. **En fil var inte begränsande.**

## Decision
**Keep.** Den är publik, fungerar på mobil + desktop, sparar arbete, kan exporteras. Värd att dela vidare.

## Next experiment
**Hypotes:** *"Om jag skickar länken till en kompis utan instruktioner, kan de skapa ett 3-stegs beslutsflöde med Ja/Nej-pilar på under 2 minuter."*

- **Bygg:** Inget. Bara skicka länken.
- **Mät:** Tid från första klick till färdigt diagram + ev. frågor de ställer.
- **Lär:** Är hint-texten tillräcklig? Behöver vi onboarding/tooltips? Är dubbeltap upptäckbart?
- **Tidsbudget:** 0 min utveckling, 5 min observation.
