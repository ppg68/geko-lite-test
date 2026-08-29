# Geko Lite — file online

Repository dei 4 file Geko Lite pubblicati online. Ogni file è un'app HTML
autonoma (HTML+CSS+JS in un unico file, dati inclusi) — non serve build,
non serve npm: si modifica il file e si pubblica con git push.

## File e cosa contengono

| File            | Coordinamento      | URL online                                              |
|------------------|--------------------|----------------------------------------------------------|
| `index.html`     | Geko test          | https://geko-lite-test.pages.dev/                        |
| `mozambico.html` | OIKOS Mozambico    | https://geko-lite-test.pages.dev/mozambico.html          |
| `zanzibar.html`  | OIKOS Zanzibar     | https://geko-lite-test.pages.dev/zanzibar.html            |
| `tanzania.html`  | OIKOS Tanzania     | https://geko-lite-test.pages.dev/tanzania.html            |

I 4 file condividono lo stesso identico codice applicativo (HTML/CSS/JS):
solo il blocco dati incorporato (`SEED_DATA`, verso l'inizio del file, tra
`/*SEED_JSON_START*/` e `/*SEED_JSON_END*/`) cambia da un file all'altro,
con i dati specifici di ciascun coordinamento.

**Prima di fidarsi del nome di un file ricevuto dall'utente**: il nome del
file NON garantisce che i dati corrispondano al coordinamento giusto (è già
successo che un file chiamato "Tanzania" contenesse dati del Mozambico o
del Ciad). Verificare sempre il campo `meta.country` dentro `SEED_DATA`
prima di usare un file come sorgente per un aggiornamento.

## Come pubblicare una modifica

1. Modificare il/i file `.html` in questa cartella (non in `Downloads` o
   altrove — questa è la cartella collegata al repository).
2. `git add <file> && git commit -m "..." && git push origin main`
3. Cloudflare Pages ricostruisce e pubblica automaticamente entro 1-2
   minuti — nessun altro passaggio manuale necessario.

Il repository GitHub è `https://github.com/ppg68/geko-lite-test` (branch
`main`), già collegato a Cloudflare Pages.

## Applicare una modifica di codice a tutti e 4 i file

Dato che i 4 file condividono lo stesso codice applicativo:
1. Individuare il blocco di codice da modificare in un file (es.
   `mozambico.html`), verificando con `grep`/`diff` che sia identico negli
   altri 3.
2. Applicare la stessa modifica (stessa stringa esatta) in ciascuno dei 4
   file, senza mai toccare il blocco `SEED_DATA` di ciascuno.
3. Verificare la sintassi JS di tutti e 4 prima di pubblicare (es. con
   `node -e` che estrae ed esegue `new Function()` su ogni `<script>`).

## Cloudflare Access (protezione login)

Dashboard: Zero Trust → Access → Applications, progetto associato al
dominio `geko-lite-test.pages.dev`. Ogni pagina protetta ha una sua
Application + policy dedicata (es. "Geko Mozambico", "Geko Zanzibar").
Al momento **Mozambico e Zanzibar hanno policy "Everyone"** (nessun login
richiesto, temporaneo) — **Tanzania non ha ancora nessuna Application**
(pagina completamente pubblica, protezione da creare quando richiesto).

## Modifiche applicate finora (cronologia sintetica)

- Spostato il pulsante "Alloca su più mesi" subito sotto "Nuova
  allocazione" nella sezione Riepilogo allocazioni.
- Sostituito il menu a tendina "Budget line" (nei modali di allocazione)
  con un campo di ricerca che filtra per prefisso del codice, ordinato.
- Aggiunto un pulsante "Salva con nome" accanto al download automatico,
  che usa la File System Access API (solo browser Chromium) per scegliere
  cartella/nome, con fallback al download normale altrove.
