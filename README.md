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

## Aggiornare risultati e classifica
I risultati sono in `dati/lega.json`, nell'elenco `giornate`. In ogni partita compila `gc` e `gf` (gol casa e fuori) e `pc` e `pf` (fantapunti casa e fuori), per esempio `"gc": 2, "gf": 1, "pc": 75.5, "pf": 70`.
Classifica e statistiche si ricalcolano da sole. L'ordine degli spareggi è in `criteri` (`pt` punti, `dr` differenza reti, `gf` gol fatti, `ptt` punti totali).

Dati e figurine provengono dall'app di fantacalcio.it.

## Credits
Sito ideato e curato da **Pinellus** · https://pinellus.github.io/fantasms2026
