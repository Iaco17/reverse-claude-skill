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

## Perché questa e non un'altra

Esistono già skill famose che fanno "pensare Claude prima di agire". Questa nasce perché nessuna di quelle fa il giro completo.

| Skill | Cosa fa | Cosa le manca rispetto a Reverse |
|---|---|---|
| **First principles thinking** (ce ne sono decine) | Ti guida con domande a ragionare sulle verità fondamentali di un problema | Ti aiuta a pensare, ma non costruisce niente |
| **Working backwards** | Il metodo di Amazon: parte dal cliente e risale al prodotto | È pensata per il product management, non per un'app, una repo o un progetto d'esame |
| **Success criteria / goal-driven** | Fissano cosa vuol dire "fatto" prima di partire | I criteri li deve dare l'utente, e sono quasi sempre pensate per il codice |
| **Superpowers: brainstorming** | Prima di scrivere codice ti fa domande e scrive un documento di design | Vale solo per il codice e le risposte le chiede a te: non va a cercare com'è fatto bene |

**Cosa fa di diverso**
- **Va a cercare fuori i criteri** invece di chiederli a te. Se non sai come lavora uno studio da commercialista, non puoi spiegarlo a Claude: Reverse lo scopre da sola.
- **Pensa a tutti quelli che giudicano**, non solo a chi userà il risultato: chi paga, chi ci lavora insieme, privacy e vincoli legali.
- **Non si fida di se stessa**: pre-mortem prima di costruire, verifica fatta da un agente separato, report con i ⚠️ invece di "tutto perfetto".
- **Vale per qualsiasi lavoro che verrà giudicato**: app, repo, profili, progetti d'esame. Non solo codice.

**Quando conviene usare le altre**
- **Programmi seriamente in Claude Code** → Superpowers ha un sistema di test e verifica sul codice molto più completo, ed è usata da migliaia di persone.
- **Devi solo ragionare su un problema**, senza costruire niente → una skill di first principles basta ed è più leggera.

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

- Costa più tempo e più ricerche di una risposta diretta: ha senso solo quando la qualità del risultato conta
- Se hai attive skill simili (per esempio il brainstorming di Superpowers), possono partire insieme e pestarsi i piedi
