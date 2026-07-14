# Siamo Tutti Europei — gioco da tavolo educativo

Gioco in un unico file HTML (`index.html`), 1–6 giocatori, bilingue IT/EN: trasporto merci attraverso l'Europa + quiz di cultura europea. Ideato da Nuccio; realizzazione tecnica con Claude.

- **Online**: https://pxh2407.github.io/siamotuttieuropei/ (GitHub Pages, repo `pxh2407/siamotuttieuropei`)
- **Copia master**: `C:\Users\Filippo\Desktop\CLAUDE\siamotuttieuropei` (clone del repo)
- Dopo ogni modifica: commit + push (il sito si aggiorna da solo in ~1 minuto)

## Stato attuale (14 luglio 2026)

- Esiste solo la versione **Con Computer** (bot 🤖 "Europa"); la versione classica è stata eliminata il 14/07/2026 (recuperabile dalla history git).
- **Tabellone equo, 75 caselle** (griglia 6×13): 15 nazioni, ognuna con 4 città + 1 dogana d'ingresso, in blocchi geografici da Italia a Portogallo, poi nave di ritorno.
- **PWA installabile** (14/07/2026): `manifest.json` + `icon-192.png`/`icon-512.png` (bandiera UE); pulsante "🖥 Inserisci un'icona sul desktop" nella schermata iniziale (usa `beforeinstallprompt`, fallback con istruzioni per iOS/Firefox; nascosto se già in modalità app). Nessun service worker (evita cache stantia). `icona.ico` serve per il collegamento sul desktop del PC di Filippo.
- **Jolly a 2 usi** (dal 14/07/2026, richiesta di Nuccio): passare la dogana senza rispondere, oppure rubare una merce. L'opzione "cambia domanda" è stata rimossa.

## Domande

- Formato: `{q:[it,en], o:[[it,en],...], a:0}` — risposta corretta SEMPRE a indice 0 (le mescola `locQ`); niente ripetizioni grazie a `pickFromPool`.
- `DOM_NAZIONE`: domande per nazione, usate alle dogane (Italia 14, Francia/Germania/Polonia 35 con le 99 domande di Nuccio, altre 5).
- `DOM_GENERALI` (48): usate per "Il Momento" e come riserva. Il 14/07/2026 aggiunte 30 domande dal doc "Segnare la crocetta sulla risposta rispondente" (diritto UE, Agenda Strategica 2024-2029, finalità UE, bilancio), tradotte in EN. NB: due soluzioni del doc erano errate/mancanti e sono state corrette (Regolamenti = diritto derivato → Falso; bilancio approvato dal solo PE → Falso).

## Meccaniche chiave

Dado + Dado Doganale (1-4 domanda, 5 Schengen raddoppia, 6 Jolly), "Il Momento" collettivo (con un 6 o sulle Arene: Berlino, Varsavia, Parigi), scambio merci su caselle blu (Milano, Riga, Bruxelles), carico max 3, contratti mai verso nazioni produttrici, scelta tra 2 contratti, cronometro 30s, vittoria a 3 contratti. Bot con difficoltà selezionabile (0.45/0.65/0.85). Salvataggio automatico in `localStorage` (chiave `steSalvataggioBot3` — va "bumpata" se cambia il percorso). Bandierine in SVG (`flagSVG`) perché le emoji-bandiera non si vedono su Windows.

## Trappole note

- Collaudo: robot JavaScript nel browser che gioca da solo; durante "Il Momento" deve cliccare in base a `pointerEvents`, non a `cur().bot`.
- Lo screenshot del Browser pane va in timeout con la pagina animata: verificare con `javascript_tool`/`read_page`.
- `renderLog` ha try/catch sulle voci (closure su stato mutato).
- Messaggi di commit multilinea: usare `git commit -F file` (gli here-string PowerShell con virgolette si rompono).
