# Collage Facce — Design Doc

## Concept
Poster interattivo in p5js che compone volti casuali sovrapponendo parti del corpo (occhi, naso, bocca, capelli, orecchie) su uno sfondo fisso. Ogni 3 secondi viene generato un nuovo volto.

## Assets
- 30 PNG con trasparenza (alpha), suddivisi in 6 categorie:
  - occhio-sx (5 varianti)
  - occhio-dx (5 varianti)
  - naso (5 varianti)
  - bocca (5 varianti)
  - capelli (5 varianti)
  - orecchie (5 varianti)
- 1 sfondo PNG (736×1104 px, senza trasparenza)
- Tutti gli asset sono 736×1104 px, già allineati per sovrapposizione

## Comportamento
- All'avvio: selezione casuale di un pezzo per categoria
- Ogni 3 secondi: rigenerazione completa del volto
- Nessun pulsante, nessun testo, nessun logo
- La pagina occupa tutto lo schermo (scalando proporzionalmente)

## Ordine di sovrapposizione (dal basso)
1. sfondo
2. capelli (dietro)
3. orecchie
4. occhio-sx
5. occhio-dx
6. naso
7. bocca
8. capelli (davanti, se necessario — da valutare se serve un doppio layer)

## Stack tecnico
- p5.js (CDN)
- HTML + CSS minimali
- Asset caricati localmente

## Criteri di successo
- Ogni 3 secondi si vede una faccia diversa e credibile
- Le parti sono allineate correttamente (nessun scollamento)
- Performance fluida anche su macchina normale (6 immagini sovrapposte)
