# Quadratura Cassa — FIDAMAR

Webdesk per la quadratura cassa giornaliera. **v1 — modalità locale**.

## Modello di utilizzo

```
┌─────────────────────────┐
│  PC PUNTO VENDITA       │
│  (apre la webdesk)      │
│                         │
│  1. Compila quadratura  │
│  2. Salva               │
│  3. Esporta Excel       │
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  CARTELLA CONDIVISA     │
│  (Google Drive / OneDrive)
│                         │
│  Riceve il file .xlsx   │
│  quadratura_AAAA-MM-GG  │
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  UFFICIO                │
│  (apre il file Excel)   │
│                         │
│  Verifica / archivia    │
└─────────────────────────┘
```

**I dati restano solo sul PC del negozio.** Nessun cloud, nessun login, nessun database esterno.

## Cosa contiene il pacchetto

- `index.html` — applicazione completa (singolo file standalone)
- `netlify.toml` — configurazione Netlify
- `README.md` — questo file

## Come funziona

L'app è autonoma. Usa CDN per le librerie (React, Tailwind, Recharts, SheetJS). Non richiede build né server.

**Storage**: i dati sono in `localStorage` del browser sul PC del negozio. Solo chi apre la pagina su quel PC li vede.

## Funzioni di export

Dal menù "Esporta" in alto a destra:

**Excel per cartella condivisa**
- Quadratura di oggi
- Quadratura del giorno selezionato
- Settimana corrente
- Mese corrente
- Tutto l'archivio

**Backup tecnico**
- Backup JSON (per ripristino completo in caso di cambio PC)

## Promemoria automatico

Se hai compilato la quadratura di oggi ma non l'hai ancora esportata, l'app mostra un banner giallo che ti ricorda di esportarla per la cartella condivisa.

## Deploy su Netlify

**Drag-and-drop (più veloce)**
1. Vai su https://app.netlify.com/drop
2. Trascina la cartella completa (o solo `index.html`)
3. Netlify ti assegna un URL `https://NOMESCELTO.netlify.app`
4. Da "Site configuration → Change site name" puoi rinominarlo

**Consigli per la sicurezza**
- Non condividere l'URL pubblicamente, dallo solo al negozio
- Il PC del negozio dovrebbe avere password al login e antivirus
- Esporta backup JSON una volta a settimana, mettilo in posto sicuro
- Se cambi PC: esporta backup JSON dal vecchio, importalo nel nuovo

## Cartella condivisa

L'app produce file `.xlsx`. Va bene qualsiasi cartella condivisa: Google Drive, OneDrive, Dropbox, SharePoint, rete locale. L'app non si interfaccia con nessuna di esse direttamente, scarica solo il file e tu lo metti dove vuoi.

Suggerimento di organizzazione:
```
Quadrature/
├── 2026/
│   ├── 01-Gennaio/
│   ├── 02-Febbraio/
│   └── ...
└── Backup/
    └── archivio_completo_AAAA-MM-GG.xlsx
```

## Operatori configurati

Fabrizio, Ilaria, Valerio. Per modificarli apri `index.html` e cerca:

```js
const OPERATORS = ['Fabrizio', 'Ilaria', 'Valerio'];
```

## Limitazioni v1

- Niente sincronizzazione cloud automatica
- Se cancelli i dati del browser perdi le quadrature locali (fai backup JSON periodici)
- Niente accesso multi-utente con login

## Prossimi step (v2)

Se nel tempo emerge l'esigenza di:
- Accesso remoto in tempo reale dall'ufficio
- Backup automatico
- Login con utenti e ruoli

Si può migrare a Supabase mantenendo invariata l'interfaccia.
