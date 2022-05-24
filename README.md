# Refactoring Showdown Workshop
Just a random workshop on refactoring 😄

## Come si svolge il workshop
Ci si divide in squadre.  
Ogni squadra ha un capitano e un computer su cui lavorare.  
Il capitano mostrerà quanto fatto al termine delle sessioni di refactoring.  
Le squadre si possono formare in vari modi: aggregandosi per linguaggio, per livello di esperienza, oppure tipo al calcetto: i capitani a turno scelgono un giocatore.  
### 24/05/2022: 2a edizione, XPUGBG Bergamo
- [XPUGBG Meetup](https://www.meetup.com/it-IT/xpugbg/events/285713930/)
- [Board Miro con appunti](https://miro.com/app/board/uXjVOyETY8s=/)
### 13/04/2022: 1a edizione, TDD Milano
- [TDD Milano Meetup](https://www.meetup.com/it-IT/TDD-Milano/events/284995543/)
- [Board Miro con appunti](https://miro.com/app/board/uXjVO9UHkwY=/)
## Come si svolge la parte pratica
È definita una lista di code smell; un refactoring applicato assegna un punteggio.  
Lo scopo per ogni squadra è ovviamente quello di ottenere il maggior punteggio possibile.  
Piccoli refactoring danno un punteggio più basso ma sono più rapidi da applicare; i refactoring più ampi sono più onerosi ma più remunerativi.  
  
Ogni refactoring assegna un punteggio in base alla complessità dello smell che risolve.  
Ad esempio se sposto un un pezzo di codice in un nuovo metodo, ottengo 3 punti.  
Un refactoring viene accettato se i test continuano a passare anche a refactoring applicato.  
Eventuali “contestazioni” (tipo “ma quello non è un refactoring…”) saranno oggetto di discussione e valutazione 🙂  

Ogni refactoring deve essere reso evidente tramite un singolo commit: nel diff del commit deve essere visibile il refactoring applicato. Nel messaggio del commit indicate il refactoring applicato, ad es: _“Sostituita stringa ‘player’ con oggetto Player (Extract Object)”_.  

## Modalità
Una volta definite, le squadre hanno 10 minuti per dare un’occhiata al codice e definire la propria strategia (ad es. farsi una lista dei refactoring applicabili, decidere quali evitare, etc.).  
Al termine di questo tempo inizia la sessione di refactoring.  
Ogni sessione dura 25’ (un pomodoro).  

Al termine delle sessioni, ogni squadra illustra i propri refactoring e si calcola il punteggio.  
Al termine della condivisione, piccola retrospettiva per confrontare strategie, refactoring applicati, impressioni ed eventuali lezioni apprese 🙂  

## Kata
Useremo il [Tennis Kata di Emily Bache](https://github.com/emilybache/Tennis-Refactoring-Kata).  

## Tips
Alcuni suggerimenti.

### Comandi Git per mostrare i refactoring
Per mostrare i refactoring nella sequenza in cui sono stati fatti bisogna tornare alla situazione iniziale e poi mostrare i commit in sequenza.  
Un ide come IntelliJ permette di fare checkout dei commit in amniera agevole, ma è possibile farlo anche da riga di comando.  

Per agevolare questa fase è possibile agire in questo modo:

1. Scarico il kata sul mio computer
2. Creo un nuovo branch, ad es. `refactoring`
3. Svolgo l’esercizio, facendo tutti i commit che mi servono

Finito l’esercizio:
4. faccio checkout del branch da cui ho staccato il mio branch, ad es. `master`
5. uso l’alias `git conext` (git checkout next) per spostarmi da commit padre a commit figlio


###  Alias git next e git conext

Supponiamo di avere un branch `master` e un branch `refactoring` con 2 commit in più:

~~~sh
$ git log
  * dd41098 - (refactoring) Rename variable (18 minutes ago) <Ferdinando Santacroce>
   * b585367 - Rename variable (19 minutes ago) <Ferdinando Santacroce>
   *   425659f - (HEAD -> master, origin/master, origin/HEAD) Merge pull request #88 from mobmentalityshow/main (5 weeks ago) <Emily Bache>
...
~~~

Torno a `master` (commit `425659f`)
~~~sh
$ git checkout master
  Switched to branch 'master'
  Your branch is up to date with 'origin/master'.
~~~

Vedo l'hash del 1° commit che ho fatto sul branch `refactoring` (commit `b585367`)
~~~sh
$ git next refactoring
  b585367e87519fab87c1e186fc1d3b07622831d3
~~~

Faccio checkout del 1° commit che ho fatto sul branch `refactoring` e vado in `detached HEAD`:
~~~sh
$ git conext refactoring
  Note: switching to 'b585367e87519fab87c1e186fc1d3b07622831d3'.
  [... omissis...]
  HEAD is now at b585367 Rename variable
~~~

Ora faccio checkout del commit successivo, il 2° che ho fatto sul branch `refactoring`:
~~~sh
$ git conext feature
  Previous HEAD position was b585367 Rename variable
  HEAD is now at dd41098 Rename variable
~~~


Questi gli alias che possiamo mettere nel file `~/.gitconfig` per agevolare il passaggio da un commit all'altro:
~~~sh
# Vedere il commit figio di quello attuale
next = "!f() { git log --ancestry-path --format=%H ${commit}..${1} | tail -1; }; f"

# Fare checkout del commit figlio
conext = "!f() { CMIT=$(git log --ancestry-path --format=%H ${commit}..${1} | tail -1) && git checkout $CMIT; }; f"
~~~

Utilizzo
~~~sh
$ git next <branch>
$ git conext <branch>
~~~


## Code Smells List
Qui [la lista dei code smell con relativo punteggio](https://docs.google.com/spreadsheets/d/1O4HLWJh111gFNJ-A_nBaak8fLH8eVRCq/).  
