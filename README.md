# 🔁 Parti dal perché

Una skill per Claude che **prima di fare un compito capisce perché va fatto e com'è fatta bene quella cosa**, poi esegue e controlla il risultato.

> *A Claude skill that works backwards: why → what "great" looks like → gap → plan → build → verify. Written in Italian.*

## Il problema

Se chiedi a Claude "fammi un'app" o "sistemami il profilo GitHub", di solito parte subito e **si inventa cosa vuol dire "fatto bene"**. Il risultato sembra curato ma è generico.

Questa skill lo costringe a fare un passo indietro, come farebbe una persona esperta.

## Come funziona

1. **Il perché**: deduce l'obiettivo vero, chi giudicherà il risultato e cosa vuol dire successo, poi te lo fa confermare con una riga
2. **Com'è fatta bene**: cerca esempi, guide e soprattutto i criteri di chi giudica, e ne ricava 5-10 criteri verificabili
   - ✔️ **Controllo A**: ha pensato a tutti i giudici (collaboratori, privacy, chi paga)? Quali criteri, se mancano, fanno buttare tutto?
3. **Gap**: confronta la situazione attuale con i criteri
4. **Piano**: interventi ordinati per impatto
   - ⏸️ **Stop** nei compiti grossi, con il ✔️ **Controllo B, pre-mortem**: "tra un mese l'hanno buttato. Perché?"
5. **Esecuzione**
6. ✔️ **Controllo C, verifica**: prova il risultato invece di rileggerlo, lo fa giudicare da un agente separato, corregge una volta sola e chiude con un report onesto ✅ ⚠️ ❌

Nei compiti piccoli salta i controlli A e B, così non diventa lenta.

## Quando parte

- **Da sola** quando chiedi di creare o migliorare app, codice, repo, profili GitHub o progetti d'esame
- **A mano** chiamandola per nome: `/reverse`
- **Non parte** sulle domande veloci ("spiegami cos'è una API")

Quando parte, la prima riga della risposta è `🔁 Reverse attiva`.

## Un esempio reale

Richiesta: *"Fammi un tool che faccia risparmiare tempo a uno studio da commercialista."*

- **Senza la skill:** un tool carino, ma con problemi strutturali che in uno studio vero si notano dal primo giorno.
- **Con la skill:** ha capito che il problema vero è **inseguire i clienti per i documenti**, ha messo la **privacy come criterio da scarto** (niente server, niente AI esterna) e nel pre-mortem ha previsto il limite "più collaboratori, più PC". Nella verifica, l'agente separato ha trovato **4 bug seri**, tra cui la **partita IVA scambiata per un numero di telefono**: i messaggi sarebbero finiti a uno sconosciuto.

## Installazione

**Su Claude (app e web)**
1. Scarica la cartella `reverse/` e comprimila in un file `.zip`
2. Vai su **Customize > Skills** e carica il file
3. Controlla che l'interruttore della skill sia acceso

**Su Claude Code**
```bash
git clone https://github.com/Iaco17/parti-dal-perche.git
mkdir -p ~/.claude/skills
cp -r parti-dal-perche/reverse ~/.claude/skills/reverse
```

## Struttura

```
reverse/
└── SKILL.md   # la skill
```

## Limiti

- È stata testata da una persona sola, su pochi compiti
- Costa più tempo e più ricerche di una risposta diretta: ha senso solo quando la qualità del risultato conta
- Se hai attive skill simili (per esempio il brainstorming di Superpowers), possono partire insieme e pestarsi i piedi
