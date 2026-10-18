# Fanta SMS Engineering

Sito statico della lega di fantacalcio: squadre e rose, calendario, classifiche di Campionato e Coppa, commenti di giornata.
Il codice sta in `index.html` e non va più toccato: i contenuti sono in file separati.

```
index.html            pagina del sito (codice)
dati/lega.json        squadre, rose, calendario e risultati
commenti/001.md ...   un file di testo per ogni commento di giornata
img/                  stemmi e figurine
```

## Pubblicazione su GitHub Pages
1. Crea un repository su GitHub (per esempio `fanta-sms-engineering`) e carica tutti i file e le cartelle di questo pacchetto.
2. In **Settings → Pages** scegli **Deploy from a branch**, branch `main`, cartella `/ (root)`, poi **Save**.
3. Dopo circa un minuto il sito è su `https://TUO-UTENTE.github.io/NOME-REPOSITORY/`.

Il sito legge i file con il browser: funziona da GitHub Pages, non aprendo `index.html` con doppio clic dal computer.

## Pubblicare un commento di giornata
1. Nel repository apri la cartella `commenti`, poi **Add file → Create new file**.
2. Chiamalo con il numero successivo all'ultimo: `001.md` il primo, poi `002.md`, `003.md`... I numeri devono essere consecutivi, senza buchi.
3. Scrivi l'intestazione tra due righe `---`, poi il testo:

```
---
titolo: Esordio da incorniciare
data: 2026-10-20
giornata: 1ª di Lega · Campionato
video: https://www.youtube.com/watch?v=XXXXXXXXXXX
---
Primo paragrafo del commento.

Secondo paragrafo, dopo una riga vuota. Si può usare **grassetto**, *corsivo* e [link](https://...).
```

4. Premi **Commit changes**. Dopo un minuto il commento è sul sito, in cima alla sezione Commenti e in Home come "Ultimo commento".

La riga `video` è facoltativa. Il video di YouTube si guarda direttamente nella pagina, con un pulsante per aprirlo su YouTube.
Il file `commenti/_esempio.md` mostra il formato ed è ignorato dal sito.

## Conferenza stampa (comunicati delle squadre)
Ogni squadra scrive da un proprio modulo Google: la squadra è «bloccata» perché il modulo non ha il campo squadra, vale il link che riceve.
1. Crea un modulo (campi: *Titolo* facoltativo, *Commento*, *Link video YouTube* facoltativo) e collegalo a un foglio Google. Non raccogliere le email.
2. Copia il modulo otto volte (**Crea una copia**), uno per squadra, tutti collegati allo stesso foglio: ogni modulo scrive in una propria scheda.
3. Nel foglio imposta **File → Impostazioni → Impostazioni internazionali: Italia** (fuso Roma), poi per ogni scheda **File → Condividi → Pubblica sul web → CSV**.
4. Incolla ogni indirizzo CSV nel campo `csv` della squadra in `dati/lega.json`.
5. Dai a ogni squadra solo il proprio link del modulo, e non pubblicarli sul sito.

Il commento va alla giornata in base all'ora di invio. Ogni giornata di Lega comincia quando finisce la precedente e si chiude il venerdì alle 00:00 dopo il suo turno di Serie A (le date, in `giornate[].data`, sono quelle della domenica): i commenti di martedì-giovedì restano quindi sulla giornata appena giocata, e da venerdì vanno alla successiva. Nelle settimane con turno infrasettimanale la giornata si chiude prima, quando parte la successiva. `lega.oreChiusura` (96 di default) sposta la chiusura. Per togliere un commento, cancella la riga nel foglio.

## Schermo per i monitor (tv.html)
Pagina a parte, non collegata al sito: `https://pinellus.github.io/fantasms2026/tv.html`. Legge gli stessi file del sito (`dati/lega.json` e i fogli delle dichiarazioni), quindi si aggiorna con lui; si rilegge da sola ogni minuto.
Ogni 10 secondi cambia diapositiva: risultati della giornata, classifica Campionato, classifica Coppa, una diapositiva per ogni partita giocata (con i marcatori) e il prossimo turno. In basso scorre la striscia con le ultime dichiarazioni.
Prima dei risultati mostra la prossima giornata. Dopo il primo risultato inserito passa alla giornata in corso.
- `?durata=15` secondi per diapositiva · `?sa=7` forza una giornata di Serie A · `?striscia=0` nasconde la striscia
- Tasti: ← → cambia diapositiva, spazio ferma, F schermo intero. Il cursore sparisce dopo qualche secondo.

I marcatori sono solo i gol di fantacalcio: nella partita ci sono tanti gol (`gol`, `rig`, `ag`) quanti sono `gc` e `gf`, quindi 0 gol per chi segna 0. Marcatori ed eventi si inseriscono in `dati/lega.json`, nella partita, con un elenco `ev` di terne [lato, tipo, giocatore]. Lato `c` casa o `f` fuori. Tipi: `gol`, `rig` (gol su rigore), `ag` (autogol), `rp` (rigore parato), `rs` (rigore sbagliato), `esp` (espulso), `amm` (ammonito), `ass` (assist), `pm` (player of the match), `cs` (portiere imbattuto). Esempio:
```
"gc": 2, "gf": 1, "pc": 78.5, "pf": 71,
"ev": [["c","gol","Lautaro"], ["c","rp","Meret"], ["f","gol","Dybala"], ["f","esp","Rabiot"]]
```

## Aggiornare risultati e classifica
I risultati sono in `dati/lega.json`, nell'elenco `giornate`. In ogni partita compila `gc` e `gf` (gol casa e fuori) e `pc` e `pf` (fantapunti casa e fuori), per esempio `"gc": 2, "gf": 1, "pc": 75.5, "pf": 70`.
Classifica e statistiche si ricalcolano da sole. L'ordine degli spareggi è in `criteri` (`pt` punti, `dr` differenza reti, `gf` gol fatti, `ptt` punti totali).

Il calendario ufficiale della Serie A 2026/27 è in `dati/lega.json`, nell'elenco `calendarioSerieA` (38 giornate con data e partite). Ogni giornata di Campionato e Coppa rimanda alla giornata reale con un link.

I risultati reali della Serie A stanno nella stessa lista: ogni partita è `[casa, fuori, gol casa, gol fuori]` (gli ultimi due si omettono se la partita non è ancora giocata). **Regola di lavoro: ogni volta che si inseriscono i risultati della lega dagli screenshot, si aggiornano anche i risultati della Serie A giocati fino a quel momento** (fonte: Sky Sport; controllare che le coppie casa-fuori coincidano con il calendario e aggiornare `aggiornato`).

Dati e figurine provengono dall'app di fantacalcio.it.

## Statistiche
La pagina `#stats` (sottomenu della Classifica) si calcola da sola dai risultati e dagli eventi già presenti: andamento della classifica (posizione e punti per giornata), «fortuna» (punti reali meno punti attesi, confrontando i gol di ogni giornata con quelli di tutte le altre squadre), record, classifiche per evento (marcatori, assist, ammoniti...) e gol per reparto. Non servono dati in più. I voti dei singoli giocatori (file di fantacalcio.it) sono per uso personale e non vanno pubblicati nel sito né nel repository.

## Credits
Sito ideato e curato da **Pinellus** · https://pinellus.github.io/fantasms2026
