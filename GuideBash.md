--- GUIDA BASH ---

La bash (Bourne Again Shell) è un'evoluzione della precedente shell usata nei sistemi operativi Unix.
Quest'ultima, a differenza delle obsoleta  shell Unix, offre una sintassi leggera e comprensibile, adatta
per lavorare con il Sistema Operativo con gran facilità. Dopo questa piccola introduzione, passiamo adesso
ai concetti fondamentali della Bash, analizzando il codice e la sintassi che possiamo usare:

- start
        dopo aver inizializzato la Bash Shell (non in tutti i SO Linux lavoriamo con la Bash Shell direttamente, ma sue varianti
    come la csh, ksh, ecc...), ricercando nel menu (ALT+SPACEBAR) o utilizzando la shortcut dedicata (CTRL+ALT+X); ci ritr-
        troveremo di fronte a un prompt dei comandi di questo tipo:

        user_name@group dir> ...

        Qui potremmo scrivere in maniera interattiva i comandi da eseguire nella nostra Shell. Utilizzarla in tale maniera però è 
    come usare in maniera interattiva Python: Non c'è gusto. Quindi, vediamo come scrivere il nostro primo script Bash. per 
        prima cosa, creiamo il file ed iniziamo ad editarlo:

        vim main.sh

        dopo questo, la prima cosa che scriviamo all'inizio del file è lo sha-bam!, scritto cosi: #!/bin/bash. Questo farà sì che
    che il nostro codice venga eseguito nella Bash Shell (visto che, come ho detto precedentemente, la shell su cui lavoriamo
    non è la Bash Shell), potendo lavorare quindi più facilmente con le variabili di sistema, comandi, ecc... Non concentrandoci
        molto sui comandi che possiamo trascrivere, visto che sono gli stessi che usiamo nel prompt dei comandi; passiamo diretta
        alla programmazione di questa Bash Shell.

- Variabili
        le variabili in bash possono essere dichiarate facilmente semplicemente scrivendo il loro nome, il simbolo dell'uguale
    e il valore a loro assegnato. Le variabili in bash non sono "verbose" e possono quindi cambiare tipo con lo  strut-
    turarsi del codice. ecco alcuni esempi:

                - Var1="String"
                - Var1=5
                - Var1=true

    per dichiarare un array possono invece utilizzare la sintassi: declare -A VarArray. Successivamente, per poterlo utilizzare,
    basterà richiamare VarArray[index]=val, per inizializzare nuovi valori al suo interno. Oltre a questo, possiamo anche utilizzare
    variabili di sistema da usare nel nostro programma, come:

        $HOME
        $PATH
        $JAVA_HOME

        Queste potranno essere richiamate senza essere inizializzate.

- Operazioni
        in bash, gli operatori si suddividono in:

        aritmetici
        condizionali
        bitwise

        per quando riguarda gli operatori aritmetici, per poterli usare, tali operazioni dovranno essere contenute in: $(( <opcode> )), in questo modo
        se devo per esempio fare un incremento di una variabile, posso invocare il comando $(( x++ )). Le operazioni che possiamo svolgere sono addizione(+)
        , sottrazione(-), divisione(/), moltiplicazione(*) e modulo (%). Successivamente, per salvare il risultato in una terza variabile, basterà inserire
        un "=" all'interno delle tonde (es. $(( 3+5=var ))). Molto importante sono anche la gestione delli spazi, come quando assegnamo ad una variabile
        un valore. 

        Per quando riguarda gli operatori condizionali, si suddividono in due categorie: "condizionali su stringhe" e "condizionali su numeri". Per quando riguarda
        i condizionali su stringhe, questi sono i classici operatori aritmetici: maggiore(>), maggiore o uguale(>=), minore(<), minore o uguale(<=), uguale(==) e non
        uguale(!=). Se tali operazioni devono pero essere eseguiti su numeri, allora gli operatori che devono essere usati sono: -gt (maggiore) -ge (maggiore o uguale), 
        -lt (minore), -le (minore  uguale), -eq (uguale), -ne (non uguale). A differenza delle stringhe, dove per poterle comparare basta richiamare:
        - [[ "STR_1" <opcode> "STR_2" ]]; then
        per i numeri, bisogna utilizzare:
        - [[ ${INT_1} <opcode buffo> ${INT_2} ]]; then
        possiamo anche concatenare queste operazioni aritmetiche usando gli operatori booleani, come AND (&&) OR (||) e NOT(!).

                Per finire, per quanto riguarda per gli operatori bitwise, sono degli operatori "speciali" che possono essere utilizzati per svolgere operazioni a livello binario
                (il nome stesso di bitwise vuol dire "bit a bit"). Gli operatori che possiamo utilizzare in questo caso sono: & (and binario), | (or binario), ! (not binario), 
                ^ (xor binario), >> (shift destro), << (shift sinistro). Questi operatori vengono utilizzati poco rispetto agli altri, ma hanno dei vantaggi come:

                - SWAP VARIABILI:
                        ${VAR 1}^=${VAR 2}
                        ${VAR 2}^=${VAR 1}
                        ${VAR 1}^=${VAR 1}

- blocchi condizionali
                Un altro argomento molto importante che dobbiamo trattare in bash sono i blocchi condizionali. Adesso, prima di approfondire, andiamo a vedere l'utilizzo della 
        variabile $?. in bash esistono una serie di variabili "speciali" che sono rappresentate da $<num o car>. Da $1 a ${...}, per esempio, abbiamo i parametri
        passati all'interno di un programma. con $# possiamo stampare il numero di parametri passati allo script. con $0 ricaviamo invece il nome dello script, ma con $? 
                invece, salviamo il valore booleano (true o false) dell'ultima operazione da noi eseguita. Se svolgessero un operazione di test, per esempio:

                [ ${INT_1} -le ${INT_2} ];

                il risultato sarà salvato in questa variabile speciale. Adesso, se noi, vogliamo scrivere un if ben formato, lo dobbiamo pero scrivere con tale sintassi:

                if [[ ${INT_1} -le ${INT_2} ]]; then
                        ...
                else if[[ <condition> ]]; then
                        ...
                else 
                        ...
                fi

                non andiamo infatti ad utilizzare una singola parentesi quadra, in quanto vogliamo far si che venga fatta l'operazione di test, e che venga subito valutata
                . "fi" alla fine serve per chiudere il blocco condizionale (opposto dell'if). Un altro costrutto condizionale importante, invece, è lo SWITCH. Come funziona
                lo switch? differentemente da un if...else, lo switch controlla il valore aritmetico di variabile, e successivamente decide quale operazione eseguire tra 
                i "casi disponibili". Perche casi? Vediamo un esempio di uno switch:

                switch ${INT_VAR}

                case 1)

                                ;;

                case 2)

                                ;;

                case *)

                                ;;

                ognuno dei numeri che si trovano dopo case rappresentano un valore possibile che può assumere INT_VAR. Per quanto riguarda l'asterisco (*) viene
                utilizzato come caso di default (INT_VAR non assume nessuno dei valori precedentemente posti). Con un doppio ;; rappresentiamo invece la fine del
                comando (un "break" negli switch...case nei linguaggi di alto livello, come java).

- cicli iterativi
                Un qualcosa di altrettanto importante sono invece i cicli iterativi. A differenza dei blocchi condizionali, come dice il nome, i cicli operativi ci permettono
                di eseguire operazioni "cicliche" su determinate variabili, (come, per esempio, se necessitiamo di seguire un controllo su tutti gli elementi di un array). Adesso, 
                quali sono i principali cicli iterativi? Vediamoli: 

                - FOR
                il ciclo for, in bash, può essere utilizzato in tre modi differenti. Che si voglia far riferimento ad un iterazione-ad-indice:

                for(( $x = <val>; $x <> <cond>; x <inc o dec> )); do
                        ...
                done

                o ad un iterazione a sequenza:

                for $x in seq(1..10); do                        for $x in ${1..10}; do
                        ...                                                                     ...
                done                                                            done

                - WHILE and UNTIL
                -- il ciclo while, invece, ha un solo modo di utilizzo. Il suo compito è quello di svolgere iterazioni finché tale condizione risulta esser vera:

                while [ ${condition} ]; do
                        ...
                done

                -- d'altra parte, con until l'iterazione del ciclo andrà avanti finché la condizione espressa sarà falsa:

                until [ ${condition} ]; do
                        ...
                done

- funzioni
        per finire, il bash possiamo andare a creare anche delle nostre funzioni personalizzate. La possibili sintassi saranno:
                - function func_name() {
                        ...
                }
                - func_name() {
                        ...
                }

        il loro funzionamento sarà identico. All'interno di queste possiamo lavorare come se stessimo eseguendo un altro script. Unica cosa, se volessimo utilizzare 
        delle variabili in locale, dovremmo dichiare ed inizializzare quest'ultime con l'uso local <var_name>=<val>. i parametri al suo interno potranno poi essere 
        passati attraverso le variabili speciali di sistema ( $1, $2, ecc... ). Se necessitiamo, come i linguaggi di alto livello, possiamo utilizzare anche il "return"
        per ritornare determinati valori dalla funzione, ma non essendo verbose bash, non ha limiti sulle variabili passate ne su come queste debbano essere ritornate.
 

--- GIT ---
