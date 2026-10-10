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

## Aggiornare risultati e classifica
I risultati sono in `dati/lega.json`, nell'elenco `giornate`. In ogni partita compila `gc` e `gf` (gol casa e fuori) e `pc` e `pf` (fantapunti casa e fuori), per esempio `"gc": 2, "gf": 1, "pc": 75.5, "pf": 70`.
Classifica e statistiche si ricalcolano da sole. L'ordine degli spareggi è in `criteri` (`pt` punti, `dr` differenza reti, `gf` gol fatti, `ptt` punti totali).

Il calendario ufficiale della Serie A 2026/27 è in `dati/lega.json`, nell'elenco `calendarioSerieA` (38 giornate con data e partite). Ogni giornata di Campionato e Coppa rimanda alla giornata reale con un link.

Dati e figurine provengono dall'app di fantacalcio.it.

## Credits
Sito ideato e curato da **Pinellus** · https://pinellus.github.io/fantasms2026
