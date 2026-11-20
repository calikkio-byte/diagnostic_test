# 2M Digital Consulting — iPhone Check Tool

Web app (un'unica pagina, nessuna dipendenza da installare) per la **verifica rapida di un iPhone dopo l'acquisto o prima della consegna a un cliente**. Funziona da Safari, si può aggiungere alla Home e **lavora anche offline**. I dati restano sul dispositivo.

## Cosa fa

14 controlli guidati, ognuno con esito **OK / Attenzione / Problema** e nota facoltativa:

| Test | Come funziona |
|---|---|
| Audio & Microfono | tono 440 Hz, sweep 100–4000 Hz, meter del microfono con picco, registrazione di 3 s e riascolto |
| Tasti fisici · Ricarica | checklist guidate (i browser non leggono questi eventi) |
| Wireless & rete | ping misurati verso 3 host + checklist Wi‑Fi, Bluetooth, SIM, chiamata, GPS |
| Touch screen | griglia colorabile con interpolazione, contatore multitouch |
| Display | colori pieni a schermo intero (pixel morti, macchie, burn‑in) |
| Fotocamere | anteprima posteriore/anteriore/elenco lenti, scatto, checklist |
| Sensori | accelerometro, giroscopio e orientamento in tempo reale (con permesso iOS) |
| Sicurezza & iCloud | Blocco attivazione, MDM, blocco operatore, IMEI segnalato |
| Parti & originalità | cronologia assistenza, viti, indicatore liquidi, display originale |
| Batteria | valutazione automatica: ≥ 85 % OK, 80–84 % Attenzione, < 80 % Problema (+ cicli e messaggi di servizio) |
| Memoria interna | confronto capacità dichiarata vs mostrata |
| Log & crash | analisi locale di file `.ips`/log con conteggio per tipo di errore |
| Info dispositivo | modello, iOS, seriale, **IMEI con verifica checksum (Luhn)** |

Inoltre:

- **Punteggio e verdetto** (Eccellente / Buono / Discreto / Da rivedere / Non idoneo se il Blocco attivazione è presente).
- **Report**: `.txt`, `.json`, condivisione dal foglio di condivisione di iOS e **PDF** tramite *Stampa*.
- **QR reale e scansionabile** con ID, dispositivo, esiti e codice di controllo (si legge con la fotocamera dell'iPhone).
- **Firma del cliente** direttamente sullo schermo, inclusa nel PDF.
- **Cronologia** degli ultimi 30 controlli (riapri, esporta, elimina) e pulsante **Nuovo** per iniziare un nuovo controllo.
- Tema chiaro/scuro automatico, schermo sempre acceso durante i test, accessibilità (tastiera, lettori di schermo).

## Pubblicazione su GitHub Pages

1. Repository → **Settings → Pages**.
2. *Source*: `Deploy from a branch`, branch `main`, cartella `/ (root)`.
3. Apri l'indirizzo `https://<utente>.github.io/diagnostic_test/` da Safari su iPhone.
4. **Condividi → Aggiungi alla schermata Home** per usarla come app, anche offline.

> Serve HTTPS (GitHub Pages lo fornisce): fotocamera, microfono e sensori non funzionano da `http://`.
> Quando pubblichi una nuova versione, cambia il numero in `CACHE` dentro `sw.js` (es. `v3`) così gli iPhone già installati si aggiornano.

## Struttura

```
index.html              app completa (HTML + CSS + JS, include il generatore QR minificato)
manifest.webmanifest    metadati per l'installazione su Home
sw.js                   service worker per l'uso offline
icons/                  icone 192, 512 e apple-touch-icon
```

## Limiti noti

Un browser non può leggere modello, numero di serie, IMEI, stato batteria o stato dei tasti dell'iPhone: per questi dati l'app guida l'operatore con checklist e campi manuali. Il controllo non sostituisce la diagnostica ufficiale Apple.

## Licenze

Generatore QR: *qrcode-generator* © Kazuhiko Arase, licenza MIT (incluso minificato in `index.html`).
