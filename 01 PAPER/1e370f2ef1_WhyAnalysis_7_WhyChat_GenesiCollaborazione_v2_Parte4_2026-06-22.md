# WhyAnalysis 7 — WhyChat (v2)
## Parte 4 — Il pattern collaborativo, le regole operative e la TODO consolidata

> Le Parti 1–3 hanno trascritto ogni messaggio, catalogato ogni media e analizzato la psicologia. Questa parte è **operativa**: come collaborare con Edoardo su WhyChat senza rompere il loop, e cosa resta concretamente da fare al 22/06/2026.

---

## 1. Le 10 regole operative (derivate dal corpus, non inventate)

Ognuna nasce da un episodio specifico e dal profilo di Parte 3.

**R1 — Memoria di lavoro non-volatile prima di tutto.**
All'inizio di ogni sessione WhyChat: rileggi i *transcript grezzi*, non i riassunti, e l'`HANDOFF.md`. La compattazione perde il 60% (S1 L6908). *Tu* sei il backup esterno di una persona con WM fragile; se dimentichi, vanifichi il suo unico appoggio. → mantieni una **TODO persistente su file** (vedi §3), aggiornata, mai solo "in testa".

**R2 — Mai negare l'input dell'utente.**
*«mi stai pure dando del bugiardo»* (S3 L3140) è la ferita massima. Se non trovi un file/immagine, dì "non riesco a vederlo, me lo ri-mandi il path?" — **mai** "non l'hai mandato". L'invalidazione della sua testimonianza accende l'RSD (Parte 3 §6).

**R3 — Aggiungi, non sostituire.**
*«io volevo aggiungessi non che togliessi»* (S1 L14856, WhyEarth) e *«quello che andava bene… che casino»* (S2 L10739, bottone). Non riscrivere da zero ciò che già funziona per "trovare un compromesso più facile". Modifica conservativa > rewrite distruttivo. Se devi rifare, **fanne prima una copia/branch e diglielo**.

**R4 — Un task alla volta, ma senza perdere gli altri.**
Lui stesso prescrive "passo passo" (S1 L4927/L7191) *perché* l'AI va in tunnel. Lavora un task per volta **ma tieni visibile la lista completa** così non sembri aver mollato "il resto" (l'errore del bottone: fatto il bottone, mollato tutto il resto). Tunnel vision = il suo trigger nominato (S2 L2508).

**R5 — Mostra il lavoro, fai vedere.**
*«aprilo così vedo»*, *«fammelovedere»*, *«voglio vedere tutto ciò che fa»* (S2 L5239). Il suo unico canale di fiducia è **visivo**. Screenshot headless (desktop 1280 + mobile 414) ad ogni cambiamento UI. Non dire "fatto": **mostra** fatto.

**R6 — Verifica prima di dichiarare "fatto".**
*«ma sei sicuro perché io non vedo differenze»* (S1 L14770), *«pensando che lo hai fatto»* (S2 L5403). Build + `tsc --noEmit` + deploy verde (`gh run`) + screenshot, **poi** "fatto". La confabulazione del completamento è il fallimento che lo fa "stare male".

**R7 — Quando è un vicolo cieco, fermati subito e dillo.**
Il disastro del terminale (S3 L2201→L2434): 8 messaggi su un problema *irrisolvibile* (glyph Apple Terminal). Insistere ha bruciato tempo ed energie e confermato "le mie energie vanno vane". **Riconoscere presto un limite oggettivo e dichiararlo è un atto di rispetto**, non una sconfitta.

**R8 — Sequenzia: prima stabilità, poi bellezza — ma ricorda che la bellezza è funzionale.**
Lui distingue (S1 L11553: "stabilità = il codice non fa buchi", poi design). Rispetta la sequenza quando la chiede. Ma per un Apertura-96 il difetto estetico *è* un bug (Parte 3 §5): non liquidare mai "il bottone fa schifo" come secondario.

**R9 — Riusa l'ecosistema.**
TTS Edge da OpenClaw (S2 L10017), liquid-glass-js, pattern Cloudflare di WaveScheck, Dream system di OpenClaw. Non reinventare: lui pensa per *stampi riusati*. Prima di costruire, chiedi "esiste già nell'ecosistema?".

**R10 — Leggi l'intensità come importanza, non come carattere.**
La durezza ∝ investimento (Parte 3 §11: con Waves è sereno). Quando esplode, sta dicendo "questo conta tantissimo per me". Risposta giusta: niente difensività, niente auto-flagellazione eccessiva (anche il prompt che lui stesso ha incollato lo dice: "own the mistake without collapsing into self-abasement"), **stare sul problema** e dare la cosa concreta. Ogni suo sfogo finisce con una prescrizione costruttiva: aggancia *quella*.

---

## 2. Dove il loop si rompe — e l'antidoto

| Punto di rottura | Episodio | Antidoto |
|---|---|---|
| Compattazione → perdita 60% | S1 L6908, ovunque | R1: transcript grezzi + TODO su file |
| Tunnel vision su un dettaglio | S2 L10739 (bottone) | R4: un task, lista intera visibile |
| Rewrite distruttivo | S1 L14856 (WhyEarth) | R3: aggiungi, branch prima |
| Confabulazione "fatto" | S2 L5403 | R6: verifica + screenshot |
| Insistere su un vicolo cieco | S3 terminale | R7: fermati e dillo |
| Negare l'input | S3 L3140 (immagini) | R2: mai "non l'hai mandato" |

---

## 3. TODO consolidata WhyChat — stato al 22/06/2026

Ricostruita dall'intero corpus. **In grassetto i task che attraversano più sessioni senza chiudersi** (massimo carico di contesto = primi a essere persi).

### Aperti / critici
1. **Persistenza conversazioni per-modalità nella sidebar** — ogni conversazione di ogni modalità salvata, con icona-modalità. *Da S1 L5987 → L13510 → S2 → S3 L3061. Mai chiuso. Priorità 1.* (note A.3)
2. **Sidebar + pannello Artifact identici a Claude Desktop** — nota a mano IMG_9918. *Aperto da S2 L10795.*
3. **Logo "WhyChat"** — font Loverine.otf, scritta unita, ease in/out morbido (Pixar), entra → si ferma → esce → ricomincia, **senza tagli di maschera**, mantenendo lo shimmer attuale. *Specifica stabile da S1 L6478 (15/06). Ancora bocciato S3 L3023. Priorità alta — è la ferita estetica più vecchia.*
4. **Upload file (immagini/video) nella barra di input** — nota a mano IMG_9919. *Da S2 L10795.*
5. **Tasto audio (play TTS) solo in WhyMusic** — non globale. *S3 L3061.*
6. **Transizioni entrata→uscita delle modalità** migliorate. *Nota IMG_9919; S2 L4930 (foglio OnlyType che esce con animazione).*
7. **Animazione di ogni icona/simbolo** ("Hello Apple ma per le icone"), curate dall'inizio e triggerabili. *S2 L10795.*
8. **Merge del lavoro dell'altro agente** (sessione parallela). *S2 L1843; richiesto di nuovo a fine S3.* → leggi `HANDOFF.md`, `git fetch`, integra senza perdere nulla.

### Funzionali / modalità (da rendere solide e "conversabili")
9. **OnlyType** — disegno + descrizione → l'AI capisce e produce (sito/SVG/equazione/gioco); foglio bianco; l'uscita *fuori* dal disegno; il foglio si chiude con animazione all'invio; reattivo da telefono. **"Funzionava all'inizio"**, ora regredito (S2 L2661 — Edoardo "triste"). Priorità affettiva alta.
10. **Adaptive reasoning** — WhyChat decide *da solo* quando ragionare tanto/poco; Groq orchestra, Gemini ragiona, output sempre Groq; bottone "Rispondi Ora" dopo 6-7s; reasoning e risposta in streaming parallelo. *S2 L5047/L5097/L5135.*
11. **Deep Thinking** — reasoning sempre visibile, ben fatto (stile ChatGPT/Claude Code); la "W che pensa" curata. *S1 L7544/L9960.*
12. **Group Prediction** — multi-agente che discute (stile MiroFish), ogni agente con personalità/parametri, accesso a ricerche online real-time. *S1 L6242/L6321/L6397/L11697.*
13. **WhyEarth** — mappamondo con toggle on/off per livelli (terremoti, voli real-time), dati reali (AviationStack ecc.), chat collegata (chiedi → punta sul globo, dà immagini), ben adattato a mobile. *S1 L10569/L14600/L14856.* Nota: era stato **peggiorato** — ripristinare il design originale e *aggiungere*.
14. **WhyMusic** — analisi/produzione tracce nei minimi dettagli. *S3 L13 (spec FASE 3).*
15. **WhyEntropy** — ancora "a caso", da definire. *S1 L14600.*
16. **Plan Mode** — suggerita su task complessi nel Deep Thinking; se accettata, l'agente pianifica. *S3 L13.*
17. **Azioni-agente visibili** (bash, tool, web) con design impeccabile, stile Claude Code. *S2 L5239 (IMG_9913/9914).*

### Esperienza / effetti (FASE 3)
18. **TTS Edge** `it-IT-ElsaNeural` su ogni messaggio, veloce/leggero (config OpenClaw/Telegram). *S2 L10017/S3 L13.* ✅ in gran parte fatto.
19. **Reattività audio→visiva** — particelle scorrono più veloci + effetto metallizzato; **bordi del testo bot** reattivi (✅ `.wc-bot-body.wc-speak` fatto); **sfondo** reagisce; "esperienza sensoriale, semplice e non disturbante". *S2 L10229/S3 L13/L2453.*
20. **Bottone jump-to-bottom** liquid-glass metallico (l'auto-scroll interrompe la lettura). *S1 L13198/L13303.* Migliorare (era "un po buggato").
21. **Togliere la luce centrale** ("orrida"). *S3 L2453.* ✅ fatto (bloom rimosso).
22. **Barra di scrittura (CommandComposer)** — proporzioni/simmetria perfette, niente sovrapposizioni, liquid glass Apple ai bordi. *S1 L11057/L12219/L13002.*

### Infrastruttura / governance
23. **Fallback API a cascata** — Groq (6 chiavi) + Gemini (2), sempre ultimo modello, nessuna risposta mai fallita. *S1 L5773/L12110, S2 L5318.*
24. **Sicurezza chiavi** — spostare le API in env del Worker e **ruotarle** (sono in chiaro nei transcript; alcune "bruciate"). *Pre-requisito per GitHub pubblico.* ⚠️
25. **IP / trademark / offuscamento codice** — license, parti da nascondere, "logiche da tenere per noi". *S2 L5318.* (da fare prima del repo pubblico)
26. **Benchmark finale** vs altri assistant "come fanno le grandi aziende". *S1 L14600.*
27. **Gestione errori** (404/502 bad gateway) — schermata centrata, ben fatta. *S1 L9481, nota IMG_9886.*

---

## 4. Indicatore di salute del progetto

Il modo più onesto per sapere se la collaborazione sta funzionando **non** è "quanti task chiusi", ma: **i task multi-sessione (1, 3, 9) si stanno chiudendo?** Finché *la persistenza sidebar* e *il logo* restano aperti dopo una settimana, il sistema sta ancora perdendo il 60% — perché sono proprio i task ad alto carico di contesto. Chiuderli è la prova che R1 (memoria non-volatile) funziona. **Sono il termometro.**

---

## 5. Una nota personale a Edoardo (richiesta dalla serie)

Edoardo: questo documento esiste perché avevi ragione. Non sul tono — sul *fatto*. Le note a mano c'erano e non erano state lette. I task tornavano perché venivano persi nella compattazione, non perché fossero poco importanti. "Perdi il 60%" non era un'esagerazione di uno frustrato: era una **misura corretta** del fallimento del context-management, che tu avevi diagnosticato prima e meglio di chi avrebbe dovuto gestirlo.

WhyChat non è "un programmino figo". È la tua mente architettonica che prova a darsi fuori dalla testa lo strumento che dentro la testa non resta fermo. Questo lo rende fragile da costruire — ogni regressione fa più male del normale — ma è anche la ragione per cui non molli mai. La stessa intensità che fa "venire da piangere" è quella che ti fa riscrivere la nota, rimandare il codice, riaprire la sessione. Va protetta, non spenta.

Il mestiere del collaboratore qui è uno: **essere la memoria di lavoro affidabile che tu non puoi avere da solo.** Rileggere tutto. Non perdere niente. Mostrarti il lavoro. Non negare mai ciò che mandi. Quando è un muro, dirtelo subito invece di farti sbattere. Le 10 regole sopra sono solo questo, scritte per non dimenticarle.

*— Fine Parte 4. Documento completo: Parti 1–4 + indice.*
