# Tesi



Universita´ del Piemonte Orientale

Dipartimento di Scienze e Innovazione Tecnologica

Corso di Studi in Informatica

Relazione per la prova ﬁnale

Implementazione di interfacce utente

vocali, touch e di conﬁgurazione per

MagicMirror

Tutore interno:

Dott. Marco Guazzone

Candidato:

Riccardo Berto

Anno Accademico 2016/17





Indice

[Abstract](#br4)

3

4

[Introduzione](#br5)

[1](#br7)[ ](#br7)[Scopi](#br7)[ ](#br7)[e](#br7)[ ](#br7)[Problemi](#br7)[ ](#br7)[Aﬀrontati](#br7)

[1.1](#br7)[ ](#br7)[Applicazioni](#br7)[ ](#br7)[del](#br7)[ ](#br7)[MagicMirror](#br7)[ ](#br7). . . . . . . . . . . . . . . . . .

[1.2](#br7)[ ](#br7)[Interfaccia](#br7)[ ](#br7)[di](#br7)[ ](#br7)[controllo](#br7)[ ](#br7)[del](#br7)[ ](#br7)[MagicMirror](#br7)[ ](#br7). . . . . . . . . . . . .

6

6

6

[2](#br10)[ ](#br10)[Tecnologie](#br10)[ ](#br10)[Implicate](#br10)

9

9

9

9

[2.1](#br10)[ ](#br10)[Prefazione](#br10)[ ](#br10). . . . . . . . . . . . . . . . . . . . . . . . . . . . .

[2.2](#br10)[ ](#br10)[Hardware](#br10)[ ](#br10). . . . . . . . . . . . . . . . . . . . . . . . . . . . .

[2.2.1](#br10)[ ](#br10)[RasperryPi](#br10)[ ](#br10). . . . . . . . . . . . . . . . . . . . . . . .

[2.2.2](#br11)[ ](#br11)[Periferiche](#br11)[ ](#br11). . . . . . . . . . . . . . . . . . . . . . . . . 10

[2.3](#br11)[ ](#br11)[Software](#br11)[ ](#br11). . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 10

[2.3.1](#br11)[ ](#br11)[Raspbian](#br11)[ ](#br11). . . . . . . . . . . . . . . . . . . . . . . . . 10

[2.3.2](#br12)[ ](#br12)[Electron](#br12)[ ](#br12). . . . . . . . . . . . . . . . . . . . . . . . . . 11

[2.3.3](#br12)[ ](#br12)[OpenCV](#br12)[ ](#br12). . . . . . . . . . . . . . . . . . . . . . . . . . 11

[2.3.4](#br13)[ ](#br13)[Google](#br13)[ ](#br13)[Speech](#br13)[ ](#br13)[API](#br13)[ ](#br13). . . . . . . . . . . . . . . . . . . . 12

[2.3.5](#br13)[ ](#br13)[Node.JS](#br13)[ ](#br13). . . . . . . . . . . . . . . . . . . . . . . . . . 12

[2.3.6](#br14)[ ](#br14)[Express](#br14)[ ](#br14). . . . . . . . . . . . . . . . . . . . . . . . . . 13

[2.3.7](#br14)[ ](#br14)[Mustache](#br14)[ ](#br14). . . . . . . . . . . . . . . . . . . . . . . . . 13

[2.3.8](#br14)[ ](#br14)[MySQL](#br14)[ ](#br14). . . . . . . . . . . . . . . . . . . . . . . . . . 13

[2.3.9](#br15)[ ](#br15)[JavaScript](#br15)[ ](#br15). . . . . . . . . . . . . . . . . . . . . . . . . 14

[2.3.10](#br15)[ ](#br15)[Python](#br15)[ ](#br15). . . . . . . . . . . . . . . . . . . . . . . . . . . 14

[2.3.11](#br16)[ ](#br16)[GitLab](#br16)[ ](#br16). . . . . . . . . . . . . . . . . . . . . . . . . . . 15

[3](#br17)[ ](#br17)[Struttura](#br17)[ ](#br17)[del](#br17)[ ](#br17)[MagicMirror](#br17)

16

[3.1](#br18)[ ](#br18)[Il](#br18)[ ](#br18)[MM](#br18)[ ](#br18)[dall’alto](#br18)[ ](#br18)[livello](#br18)[ ](#br18). . . . . . . . . . . . . . . . . . . . . . . 17

[3.2](#br19)[ ](#br19)[Avvio](#br19)[ ](#br19)[ed](#br19)[ ](#br19)[Esecuzione](#br19)[ ](#br19). . . . . . . . . . . . . . . . . . . . . . . 18

[3.2.1](#br20)[ ](#br20)[Il](#br20)[ ](#br20)[ﬁle](#br20)[ ](#br20)[di](#br20)[ ](#br20)[Conﬁgurazione](#br20)[ ](#br20). . . . . . . . . . . . . . . . . . 19

[3.3](#br21)[ ](#br21)[Implementazione](#br21)[ ](#br21)[di](#br21)[ ](#br21)[un’applicazione](#br21)[ ](#br21). . . . . . . . . . . . . . . 20

1





[3.4](#br22)[ ](#br22)[Messaggistica](#br22)[ ](#br22)[del](#br22)[ ](#br22)[MM](#br22)[ ](#br22). . . . . . . . . . . . . . . . . . . . . . 21

[4](#br23)[ ](#br23)[Applicazioni](#br23)[ ](#br23)[per](#br23)[ ](#br23)[il](#br23)[ ](#br23)[MM](#br23)[ ](#br23)22

[4.1](#br23)[ ](#br23)[Modulo](#br23)[ ](#br23)[per](#br23)[ ](#br23)[comandi](#br23)[ ](#br23)[vocali](#br23)[ ](#br23). . . . . . . . . . . . . . . . . . . . 22

[4.1.1](#br24)[ ](#br24)[Comunicazione](#br24)[ ](#br24)[con](#br24)[ ](#br24)[l’API](#br24)[ ](#br24)[di](#br24)[ ](#br24)[Google](#br24)[ ](#br24). . . . . . . . . . . 23

[4.1.2](#br26)[ ](#br26)[Diﬃcolt`a](#br26)[ ](#br26)[incontrate](#br26)[ ](#br26). . . . . . . . . . . . . . . . . . . . 25

[4.2](#br26)[ ](#br26)[Modulo](#br26)[ ](#br26)[con](#br26)[ ](#br26)[Touch](#br26)[ ](#br26)[Board](#br26)[ ](#br26). . . . . . . . . . . . . . . . . . . . . 25

[5](#br29)[ ](#br29)[Interfaccia](#br29)[ ](#br29)[web](#br29)[ ](#br29)[di](#br29)[ ](#br29)[conﬁgurazione](#br29)

28

[5.1](#br29)[ ](#br29)[Struttura](#br29)[ ](#br29)[dell’interfaccia](#br29)[ ](#br29)[Web](#br29)[ ](#br29)[di](#br29)[ ](#br29)[conﬁgurazione](#br29)[ ](#br29). . . . . . . . 28

[5.2](#br30)[ ](#br30)[Individuazione](#br30)[ ](#br30)[e](#br30)[ ](#br30)[visualizzazione](#br30)[ ](#br30)[dei](#br30)[ ](#br30)[moduli](#br30)[ ](#br30)[nell’interfaccia](#br30)[ ](#br30). . 29

[Conclusione](#br33)

[Bibliograﬁa](#br34)

32

33

2





Abstract

La tesi aﬀronta alcune problematiche presenti al giorno d’oggi in molti proget-

ti informatici, dovute al continuo sviluppo di metodologie di interfacciamento

sempre piu` dirette e complesse. Il software nel quale sono state aﬀrontate

queste problematiche `e il MagicMirror, un progetto di domotica.

In particolare il problema `e stato implementare metodi alternativi di inter-

facciamento, rispetto a mouse e tastiera, e metodi per conﬁgurare il software

da remoto da parte di utenti non esperti.

Per aﬀrontare il primo problema sono state implementate due interfacce uten-

te: una vocale, per permettere l’impartizione di comandi tramite speciﬁche

frasi, e una touch, per eseguire speciﬁche operazioni tramite movimenti delle

dita su un’area di un dispositivo. Per il secondo problema `e stata sviluppata

un’interfaccia web di conﬁgurazione remota che permettesse di modiﬁcare

facilmente le impostazioni del software principale.

Per le interfacce utente di controllo sono stati utilizzati servizi esterni al-

l’ambiente in cui `e stato sviluppato il progetto. Per l’interfaccia web di

conﬁgurazione, invece, sono state usate tecnologie per la maggior parte gi`a

implementate nel software principale.

3





Introduzione

Nello stage che ho svolto presso Lab121 ho esteso il [\[19\]MagicMirror](#br35)[ ](#br35)(abbre-

viato in MM ), un software di domotica sviluppato da Michael Teeuw, che

gira sul calcolatore portatile Raspb[erryPi\[3\],](#br34)[ ](#br34)sul quale ho svolto due princi-

pali attivit`a:

• Lo sviluppo di applicazioni (dette anche Moduli) mirate al controllo del

MagicMirror tramite l’impartizione di comandi vocali o input trasmessi

dal movimento delle dita su una periferica touchpad.

La scelta dello sviluppo di queste applicazioni `e stata presa con l’obbiet-

tivo di dotare il MagicMirror di un’interfaccia uomo-macchina avanza-

ta. Infatti, negli ultimi decenni, con lo sviluppo di nuove tecnologie,

sono stati sviluppati ed evoluti metodi non tradizionali per il controllo

di dispositivi.

Per esempio si possono osservare la maggior parte degli Smartphone

moderni che permettono lo sblocco dello schermo con il riconoscimen-

to del volto oppure l’interazione con esso tramite sintesi vocale, invece

dell’utilizzo di tastiere analogiche o digitali. Inoltre il progresso tecno-

logico di calcolatori e periferiche sempre piu` piccoli ed economici, ha

permesso la nascita di una moltitudine di progetti casalinghi in ambito

interazione uomo-macchina, contribuendo alla crescita dei software di

questo tipo, oggi reperibili in quantita` anche open source.

• Lo sviluppo di un’interfaccia graﬁca web, la quale, tramite un pannello

di amministrazione, permette di modiﬁcare il ﬁle di conﬁgurazione del

MM e delle applicazioni che si appoggiano su di esso, evitando cos`ı di

dover accedere a ﬁle potenzialmente critici ed eliminarne parti essenzia-

li ad opera di utenti non esperti. Infatti, oltre alle tecnologie, un altro

aspetto che si `e evoluto negli ultimi anni nel campo delle Applicazioni

Web, `e l’implementazione di interfacce graﬁche di amministrazione ad

4





alto livello sempre piu` intuitive e facili da comprendere. Capita spesso

che, in assenza di queste interfacce piu` evolute, un utente inesperto sia

costretto ad utilizzare interfacce a basso livello (come strumenti di linea

di comando o ﬁle di conﬁgurazione), con il rischio di causare potenziali

danni.

Nei prossimi capitoli:

• Nel capitolo [1](#br7)[ ](#br7)verranno trattati scopi e problemi aﬀrontati nello stage

• Nel capitolo [2](#br10)[ ](#br10)verranno elencate e spiegate le tecnologie che sono state

utilizzate durante lo stage

• Nel capitolo [3](#br17)[ ](#br17)verra` spiegata la struttura del MagicMirror

• Nel capitolo [4](#br23)[ ](#br23)verranno spiegati i moduli creati per il MagicMirror

• Nel capitolo [5](#br29)[ ](#br29)verra` esposto il funzionamento dell’interfaccia web di

amministrazione

5





Capitolo 1

Scopi e Problemi Aﬀrontati

In questo capitolo verranno esposti gli scopi e i problemi incontrati durante

l’attivita` di stage divisi in due argomenti. In particolare si tratta lo sviluppo

delle applicazioni per il MM (sezione [1.1)](#br7)[ ](#br7)e lo sviluppo dell’interfaccia web

di amministrazione (sezione [1.2).](#br7)

1.1 Applicazioni del MagicMirror

Il MagicMirror `e un software che espone API, le quali permettono l’inte-

grazione di applicazioni sviluppate da terzi e forniscono funzionalit`a per la

comunicazione, gestione ed organizzazione tra le applicazioni. Lo scopo nello

sviluppo delle applicazioni, durante lo stage, `e stato di creare programmi

che permettessero l’interazione tra il software principale e l’essere umano.

Nello speciﬁco si `e voluto implementare la possibilita`, da parte di un utente,

di controllare le applicazioni attive sul MagicMirror tramite l’impartizione di

comandi vocali o movimenti delle dita su una scheda Touch Board. In questa

parte si `e dovuto aﬀrontare il problema di far comunicare i diversi disposi-

tivi hardware con il calcolatore principale, e di programmare le applicazioni

con linguaggi diversi, a seconda della compatibilit`a di un linguaggio e delle

librerie a disposizione di una determinata periferica.

1.2 Interfaccia di controllo del MagicMirror

Il MM possiede all’interno delle sue cartelle un ﬁle di conﬁgurazione, il quale

permette di conﬁgurare sia MM che le applicazioni caricate su quest’ultimo.

6





Prima dello stage per modiﬁcare la conﬁgurazione, bisognava accedere di-

rettamente al ﬁle di conﬁgurazione appena presentato e modiﬁcarlo. Questo

approccio, oltre ad essere scomodo, puo` anche causare errori, dal momento

che `e necessaria una sintassi corretta all’interno del ﬁle.

Preso atto di questo, nella seconda parte dello stage si `e svolta la progettazio-

ne e lo sviluppo di un’interfaccia Web di conﬁgurazione remota il cui scopo `e

di permettere ad un utente autenticato di gestire le conﬁgurazioni del MM,

e dei moduli implementati su di esso, da una pagina web anzich`e accedendo

alla macchina ﬁsica su cui gira l’applicazione. L’interfaccia permette anche

di disattivare (o attivare) le applicazioni presenti nel MM, la cui procedura,

prima, richiedeva di aggiungere manualmente un pezzo di codice nella con-

ﬁgurazione del software principale. Lo scambio dei messaggi tra il MM e la

pagina web avviene in formato JSON, lo stesso formato usato per il ﬁle di

conﬁgurazione.

Un altro problema riscontrato in questa parte `e stata la diﬃcolta` dell’uti-

lizzo di Javascript perch`e `e un linguaggio orientato ad eventi, ovvero alcune

funzioni vengono eseguite senza attendere il risultato della precedente. Il lin-

guaggio, per poter sincronizzare le funzioni, mette a disposizione le callback:

esse sono funzioni passate come parametro ad un’altra funzione, cosicch´e

quest’ultima pu`o svolgere un determinato compito (quello svolto nella call-

back) che non `e noto al momento della scrittura del codice. Senza buone

pratiche di programmazione si rischia di incontrare un fenomeno chiama-

to ”CallbackHell”, ovvero callback che chiamano a loro volta altre callback

creando funzioni annidate piu` volte, come mostrato in ﬁgura [1.1.](#br9)

7





Figura 1.1: Esempio di CallbackHell

Nella ﬁgura il codice esegue delle query attraverso delle API esposte da

un servizio. La funzione CallEndpoint() chiama la funzione dell’API pas-

sandogli un percorso, il quale restituisce il risultato di una query. Per poter

procedere a quella successiva `e richiesto il risultato della precedente e per

farlo `e necessario l’utilizzo di un’altra callback. Questa dipendenza si ripre-

senta anche nelle query successive creando un annidamento sempre maggiore

conosciuto come CallbackHell.

8





Capitolo 2

Tecnologie Implicate

In questo capitolo verranno discusse le tecnologie che sono state studiate ed

utilizzate durante le attivita` di stage. In particolare il capitolo `e diviso tra

tecnologie hardware e tecnologie software.

2.1 Prefazione

Lo sviluppo del progetto di stage `e stato svolto nell’ambiente [Raspbian\[1\],](#br34)

una distribuzione [Debian\[2\]](#br34)[ ](#br34)che gira sul dispositivo Raspe[rryPi\[3\].](#br34)[ ](#br34)Inoltre

sono state adottate diverse tecnologie nel campo del riconoscimento vocale

e di immagini (OpenCV [\[4\]](#br34)[ ](#br34)e Google Speech API [\[5\]),](#br34)[ ](#br34)nello sviluppo di

applicazioni web (Electron [\[6\],](#br34)[ ](#br34)Node.JS [\[14\],](#br34)[ ](#br34)Express [\[8\],](#br34)[ ](#br34)Mustache [\[10\])](#br34)[ ](#br34)e

della gestione dati (MySQL [\[9\]).](#br34)[ ](#br34)Inoltre sono stati adottati diversi linguaggi

di programmazione (JavaScript [\[11\],](#br34)[ ](#br34)Python [\[12\]).](#br34)[ ](#br34)Inﬁne, per la gestione

distribuita di progetti software e di versionamento del codice, `e stata usata

la piattaforma GitLab [\[13\].](#br34)

2.2 Hardware

2.2.1 RasperryPi

RaspberryPi `e un calcolatore elettronico, montato su una singola scheda

elettronica, caratterizzato dal basso costo, dal consumo energetico ridotto

e, per le sue dimensioni ridotte, dalla facile portabilit`a. Rilasciato per la

prima volta nel 2012 `e diventato un prodotto utilizzato per una moltitudine

di progetti sia aziendali che casalinghi. Il modello usato durante lo stage `e

RaspberryPi 3 model B e monta:

• CPU con architettura Advanced RISC Machine (ARM)

9





• 1 porta HDMI

• 1 porta LAN

• 1 uscita Aux

• 4 porte USB

• 40 pin General Purpose Input/Output(GPIO)

• 1 scheda di rete wireless

• Alimentazione microUSB 5V

• un bus camera serial interface(CSI), ovvero una porta per telecamera

con Flexible ﬂat cable(FFC)

• ingresso per microSD

Il sistema operativo per Raspberry deve essere installato su una microSD op-

portunamente formattata e conﬁgurata con un Master Boot Record (MBR).

2.2.2 Periferiche

Nella creazione delle applicazioni per il Magic Mirror sono state usate diverse

periferiche, tra cui un microfono USB, per catturare la voce in input e un

componente Skydriver Touch Board (94mm x 122mm) di Piromoni collegabi-

le tramite i 40 pin GPIO del calcolatore principale, per catturare input ﬁsici

tramite il movimento delle dita sulla Touch Board.

2.3 Software

2.3.1 Raspbian

Raspbian `e una distribuzione del sistema operativo Linux derivata da De-

bian, completamente libera, ottimizzata per Raspberry. Fu sviluppata da

Mike Thompson e Peter Green come progetto non aﬃliato alla compagnia

RaspberryPi Fundation, per tenere in considerazione la limitata capacit`a di

calcolo dei processori ARM. La prima versione venne rilasciata nel 2012.

10





2.3.2 Electron

Electron `e un framework open source rilasciato per la prima volta nel 2013,

`

ma la prima versione stabile `e uscita nel giugno 2017. E disponibile per i si-

stemi operativi Windows, MacOS e Linux ed `e scritto in C++ e Javascript. Il

framework permette la creazione di applicazioni multipiattaforma utilizzando

tecnologie gia` esistenti per lo sviluppo del lato client e del lato server (Java-

script, Node.JS, V8 [\[15\]).](#br34)[ ](#br34)All’avvio di Electron viene inizializzata una pagina

con Chromium [\[17\](un](#br34)[ ](#br34)web browser installato insieme all’applicazione) nel

quale viene mostrata una pagina web, e un server in Node.JS. Un’applicazione

sviluppata con Electorn ha bisogno di 3 componenti principali:

• Il package.json, un ﬁle JSON, che deve contenere almeno il nome del-

l’applicazione, la versione dell’applicazione creata, la descrizione di que-

st’ultima e il nome del ﬁle principale dell’applicazione (necessaria per

l’avvio), come mostrato nella seguente immagine:

1 {

2

”name” : ” magicmirror ” ,

” version ” : ”2.1.1” ,

3

4

5

” description ” : ”The open source smart platform ” ,

”main” : ” j s / electron . j s ”

6 }

Name `e il campo che assegna il nome dell’applicazione, version `e il cam-

po che assegna la versione dell’applicazione, description `e una stringa

che descrive il programma, main `e il campo che punta al ﬁle Javascript

da eseguire all’avvio.

• Un ﬁle HTML che contiene il template della pagina generata dall’ap-

plicazione

• Un ﬁle JavaScript che contiene il codice di esecuzione dell’applicazione

come ad esempio la creazione di una ﬁnestra o la visualizzazione di una

pagina.

2.3.3 OpenCV

OpenCV (Open Source Computer Vision Library) `e una libreria software

sviluppata intorno al 2000 utilizzata nell’ambito della visione artiﬁciale per

l’acquisizione e il riconoscimento di immagini da parte di una macchina per

mezzo di input digitali, ottenuti tramite telecamera o fotocamera.

La libreria `e disponibile per i linguaggi C++(linguaggio in cui `e scritta), C,

11





Python e Java e per diversi sistemi operativi, compresi quelli speciﬁci per i

dispositivi mobili.

OpenCV prende in input un’immagine o uno stream (come un video o una

serie di immagini) e, utilizzando speciﬁci algoritmi di Machine Learning, `e in

grado di individuare e riconoscere oggetti speciﬁci.

2.3.4 Google Speech API

Negli ultimi anni Google ha ampliato sempre di piu` il suo catalogo per quanto

riguarda i servizi cloud e web API. Tra questi si pu`o individuare anche Google

Speech API, il quale `e un servizio che, ricevendo in input un ﬁle o uno stream

audio, ottenuto per mezzo di un’acquisizione da un dispositivo di audio input,

traduce il parlato in testo scritto tramite algoritmi avanzati di riconoscimento

della voce.

L’API supporta oltre 110 lingue e si possono usare su diverse piattaforme

dato che le librerie sono disponibili nei linguaggi C#, GO, Java, Node.JS,

PhP, Python e Ruby. Inoltre Google Speech API dispone di alcune varianti:

• Una con interfaccia REpresentational State Transfer(REST), che co-

munica per mezzo di URI

• Una con gRPC, un sistema di chiamata di procedura remota

2.3.5 Node.JS

Node.JS gi`a distribuito con Electron, ed `e stato usato per la creazione del ser-

ver per la gestione dell’interfaccia web per il MM. Node.JS `e una piattaforma

open source che permette l’esecuzione del linguaggio Javascript, sfruttando il

motore JavaScript V8 sviluppato da Google, anche per il lato server, ovvero

la parte del sistema che `e adibita alla manipolazione e all’elaborazione dei

dati in modo completamente trasparente all’utente.

Node.JS esegue delle operazioni al veriﬁcarsi di uno speciﬁco evento, che puo`

essere un accesso ad una porta del server o la richiesta di una pagina.

Per gestire i pacchetti di questo framework viene utilizzato [NPM\[16\],](#br34)[ ](#br34)uno

strumento che permette di scaricare ed installare librerie private o pubbliche

salvate su un database.

12





2.3.6 Express

Express `e un framework per Node.JS che permette di creare applicazioni

Web in JavaScript, oﬀrendo strumenti e pacchetti che implementano piu`

facilmente tutte le funzionalita` oﬀerte da Node.JS. Il software viene usato

per creare e gestire il back-end di un server, che `e composto da 3 entit`a

importanti:

• il Controller, che deﬁnisce le funzioni associate ad un determinato

modello.

• il Routing, utilizzato per determinare come il server debba rispondere

ad un determinato metodo di richiesta, ricevuta sottoforma di URI,

inoltrando la stessa alla funzione del controller del rispettivo modello

a cui fa rifermento.

• i Modelli, creati per ogni entit`a-oggetto che esiste all’interno del server,

ad ognuno dei quali viene associato un controller. Inoltre, tramite i mo-

delli si accede al database per estrarre i dati e spedirli al controller per

la manipolazione, ricevendoli successivamente modiﬁcati e salvandoli,

se necessario.

2.3.7 Mustache

Mustache `e un sistema di template, ovvero un sistema che prendendo in input

dati e web template genera automaticamente pagine web, permettendo cos`ı

di riutilizzare elementi statici dei template. Dal momento che Mustache `e

disponibile in diversi linguaggi tra cui Javascript `e stato usato per l’interfac-

cia web di conﬁgurazione del MagicMirror. Mustache `e un sistema logic-less

perch`e `e privo di istruzioni per il controllo del ﬂusso (come ad esempio l’”if”

e l’”else”), quindi tutti i controlli di questo tipo sono data-driven.

2.3.8 MySQL

MySQL `e stato usato durante lo stage come database per l’archiviazione di

account di utenti accreditati all’autenticazione per accedere all’interfaccia

web di conﬁgurazione del MM.

MySQL `e uno tra i piu` famosi database open source sviluppato da Oracle,

13





piu` precisamente `e sistema per la gestione di basi di dati basato sul modello

relazionale. MySQL `e composto da una semplice riga di comando e un ser-

ver web, ma sono implementati anche programmi per l’amministrazione del

database come, ad esempio, il famoso phpMyAdmin. La prima versione fu

rilasciata nel maggio del 1995 sviluppata da Oracle e di proprieta` di MySQL

AB, distribuito sia con licenza commerciale sia con licenza libera.

2.3.9 JavaScript

Javascript `e un linguaggio di programmazione ad alto livello orientato agli

oggetti e ad eventi, che `e supportato dalla maggior parte dei browser per lo

scripting delle pagine web, e che supporta la programmazione procedurale.

Inizialmente usato per il lato client ha subito un’evoluzione che lo ha portato

ad essere utilizzato per lo sviluppo di back-end e web app.

ECMAJavascript(ES) `e lo standard di Javascript che negli ultimi anni ha

sviluppato ed evoluto il linguaggio in diverse versioni. Uno degli aspetti su

cui il processo di standardizzazione si focalizzato `e la sempliﬁcazione della

gestione degli eventi e delle funzioni asincrone (cio`e di quelle che riconse-

gnano il controllo al chiamante prima della loro terminazione). Le pratiche

utilizzate per sincronizzare queste funzioni in ECMAJavascript 5 (ES5), ov-

vero la versione usata durante lo stage, sono l’utilizzo delle callback.

In ECMAJavascript 6 (ES6) `e stato introdotto il concetto di Promises, che ha

sostituito le funzioni di callback. Una Promise rappresenta un proxy per un

valore non necessariamente noto quando la Promise `e stata creata. Questa

consente di associare degli handlers con il successo o il fallimento di un’azione

asincrona, restituendo il valore prodotto, nel primo caso, o la motivazione nel

secondo.

Sono tutt’ora in via di sviluppo nuove versioni di Javascript.

2.3.10 Python

Python `e un linguaggio di programmazione open source, ad alto livello, con

semantica dinamica, orientato ad oggetti, usato per lo sviluppo di applica-

zioni e scripting.

Questo linguaggio `e stato particolarmente utile per l’interfacciamento con

la telecamera e la Touch Board, essendo a disposizione librerie apposite per

gestirle.

14





Come molti altri linguaggi, supporta l’implementazione di pacchetti esterni

che possono essere salvati in una repository pubblica o su piattaforme ester-

ne. Nel primo caso Python utilizza un suo gestore di pacchetti: Pip Installs

Packages o Pip Installs Python (pip, acronimo ricorsivo). Nel secondo caso i

pacchetti possono essere inseriti senza dover utilizzare il gestore di pacchetti

appena introdotto.

2.3.11 GitLab

GitLab `e una piattaforma web che implementa le funzionalit`a oﬀerte dal

software Git e altri servizi tra i quali la possibilit`a di creare wiki e un servizio

di issue tracking, utile per tenere traccia di eventuali richieste o problemi.

La comodita` di questa piattaforma sta nel poter creare dei Commit, ovvero

ad ogni modiﬁca del codice si pu`o salvarne lo stato assegnandoli un’etichetta

in locale, per poi spedirlo al respository in remoto del progetto. In ogni

momento si puo` tornare ad una versione vecchia tramite gli strumenti di

versionamento oﬀerti dalla piattaforma web.

15





Capitolo 3

Struttura del MagicMirror

Il MagicMirror (detto anche MM ) `e un progetto ideato e sviluppato da Mi-

chael Teeuw, successivamente esteso nelle sue funzionalita` da una moltitudi-

ne di utenti su GitHub. La prima versione `e stata scritta completamente in

Python, mentre nella versione successiva `e stato utilizzato Electron, che ha

comportato una variazione di linguaggio, a favore di Javascript. In questo

modo `e stato possibile implementare un’interfaccia esteticamente piu` grade-

vole e API piu` intuitive. L’idea dell’autore `e nata rifacendosi allo specchio

magico della rinomata ﬁaba scritta dai fratelli Grimm: Biancaneve e i Sette

Nani.

Il software viene mostrato attraverso un comune monitor, trasmettendo im-

magini poste su uno sfondo completamente nero. Applicando sopra una

semplice pellicola a specchio (la quale da un lato permette di specchiarsi e

dall’altro di vedere attraverso) si crea un eﬀetto particolare per cui una per-

sona riesce a specchiarsi e allo stesso tempo riesce a vedere le scritte o le

immagini trasmesse dal monitor, come mostrato in ﬁgura [3.1.](#br18)[ ](#br18)In quest’ulti-

ma si pu`o vedere il MM che, oltre alla sua funzione base di specchio, mostra

alcune informazioni come l’ora, la temperatura, il meteo e un messaggio.

In questo capitolo verr`a spiegata la struttura generale del MM (sezione [3.1),](#br18)

le classi principali che vengono caricate all’avvio (sezione [3.2),](#br19)[ ](#br19)la struttura

del ﬁle di conﬁgurazione (sezione [3.2.1),](#br20)[ ](#br20)come viene implementata un’appli-

cazione (sezione [3.3)](#br21)[ ](#br21)e il funzionamento del sistema di messaggistica (sezione

[3.4).](#br22)

16





Figura 3.1: MagicMirror by Michael Teeuw

3.1 Il MM dall’alto livello

Il MM `e una applicazione composta da diversi componenti software con cui

`e possibile comunicare attraverso le API messe a disposizione da MM. Si

possono individuare alcuni elementi principali rappresentati in ﬁgura [3.2:](#br19)

17





Figura 3.2: Struttura MagicMirror

• Il core, il cuore del MM dove gira il codice principale.

• Il server, che gira in locale, usato per restituire la pagina HTML, con i

dati, al browser di Electron e comunicare con le API

• I Moduli, entit`a che espone le API per l’implementazione di applicazioni

• I NodeHelper, entita` che espone le API per l’implementazione di fun-

zioni di supporto al Modulo

• Il Socket, entit`a che fornisce un canale di comunicazione tra i Moduli

• Il SocketClient, entita` che fornisce un canale di comunicazione tra un

Modulo e il proprio NodeHelper.

3.2 Avvio ed Esecuzione

Il MM viene avviato tramite linea di comando, la quale esegue il codice di

un ﬁle Javascript, il cui percorso `e indicato nel documento package.json di

18





Electron, descritto nella sezione [2.3.2.](#br12)[ ](#br12)Il ﬁle contiene il codice di Electron, che

si occupa dell’avvio di MM, caricandone tutte le strutture, e della creazione di

una nuova ﬁnestra browser, il cui compito `e di mostrare l’output dei moduli.

La pagina costruita e l’output dei moduli sono un insieme di Document

Object Model (DOM), ovvero oggetti HTML che compongono una pagina

web, i quali vengono mostrati solo dopo l’avvio di tutti i moduli attivi.

Le strutture principali caricate dal MM sono le seguenti:

• gli end-point delle API per le applicazioni, che sono le interfacce usate

per leggere e caricare le applicazioni inserite nel MM.

• gli end-point delle API per la gestione dei NodeHelper. Sono strutture

opzionali usate per collegamenti esterni al MM (per esempio, con API di

un servizio cloud). Ogni applicazione ha il proprio NodeHelper con cui

puo` comunicare tramite messaggi in modo simile a come comunicano

le applicazioni tra di loro.

• un ”Socket” e un ”Socket-Client”, entita` principali che deﬁniscono le

funzioni per lo scambio dei messaggi tra le applicazioni e i rispettivi

NodeHelper.

• un Logger, implementato per tenere i log dell’applicazione e degli even-

tuali errori. Usato principalmente per il debugging.

• un ﬁle di conﬁgurazione, nel quale sono speciﬁcati il nome e le coordi-

nate per la posizione dei vari moduli all’interno della pagina.

Inoltre viene inizializzato un server, il cui compito `e quello di trasmettere la

pagina HTML generata, con gli output delle varie applicazioni, al browser

precedentemente avviato.

3.2.1 Il ﬁle di Conﬁgurazione

Come discusso nella sezione [1.2,](#br7)[ ](#br7)il MM carica un ﬁle di conﬁgurazione, che

`e composto dai seguenti campi:

• la porta del server

• una whitelist, ovvero un IP oppure un range di IP che possono collegarsi

allo specchio

19





• la lingua principale del sistema

• il formato dell’ora (12h o 24h)

• l’unita` di misura (ad esempio pixel), usata per gestire la distanza degli

oggetti HTML

• una lista di moduli (in formato JSON) da caricare durante l’avvio del

MM con la relativa posizione nella pagina. Per ogni applicazione de-

ve necessariamente comparire il nome e la posizione; opzionalmente

si possono inserire un campo header e un campo conﬁg speciﬁco per

l’applicazione, come mostrato nell’esempio in ﬁgura [3.1.](#br21)

1 {

2

3

”module” : ’ nome dell ’ applicazione ’ ,

” position ” : ’ la posizione dell ’ applicazione

all ’ intenro d e l l o specchio ’ ,

4

”header” : ’ una stringa che viene stampata

sopra all ’ applicazione ’ ,

5

6 }

” config ” : { opzioni varie in formato JSON }

Listing 3.1: Campi di conﬁgurazione di un modulo nel MM

La lingua, il formato dell’ora e l’unit`a di misura usata sono parametri messi

a disposizione dal sistema per la creazione di un’applicazione (ad esempio, il

display di un orologio).

3.3 Implementazione di un’applicazione

La modiﬁca del ﬁle di conﬁgurazione del MM appena descritta serve per

”notiﬁcare” la presenza delle applicazioni a quest’ultimo, ma perch`e possano

funzionare `e necessario che rispettino alcune speciﬁche regole. Per inserire

il codice dell’applicazione all’interno dello specchio `e necessario creare una

cartella con un nome identiﬁcativo dell’applicazione nella directory Modules.

Dentro la cartella appena creata devono essere inseriti:

• 1 ﬁle Javascript (JS), ovvero il documento principale con lo stesso nome

della cartella appena creata. Contiene il codice dell’applicazione, il

quale conterr`a a sua volta il codice per la creazione dei DOM

• 1 ﬁle Cascading Style Sheets (CSS), per modiﬁcare l’estetica del DOM

della relativa applicazione (opzionale)

20





• 1 ﬁle node helper.js, che `e il NodeHelper associato alla speciﬁca appli-

cazione (opzionale)

• Altri ﬁle necessari all’applicazione (immagini, JSON, etc)

3.4 Messaggistica del MM

Nella sezione [3.1](#br18)[ ](#br18)`e stato gia` accennato che il MM implementa un meccanismo

di messaggistica sfruttando un sistema di socket integrato, utile per l’orga-

nizzazione e la moderazione delle applicazioni tramite l’utilizzo di funzioni

messe a disposizione dall’API. Sono presenti due classi socket:

• Socket, classe che fornisce le funzioni per ricevere e mandare messaggi

tra i moduli del MM. Con questo socket la spedizione del messaggio `e

in broadcast usando il metodo sendNotiﬁcation(notiﬁcation, payload).

Il primo parametro `e una stringa che identiﬁca il messaggio, il secondo

parametro `e opzionale e pu`o essere usato per inserire il corpo del mes-

saggio. La ricezione del messaggio viene gestita con il metodo notiﬁca-

tionReceived(notiﬁcation, payload, sender), i primi due parametri sono

uguali a quelli della funzione per spedire, il terzo parametro contiene il

nome del modulo che ha mandato il messaggio

• SocketClient, classe che fornisce le funzioni per ricevere e mandare

messaggi tra il modulo e il suo NodeHelper. Per spedire i messaggi

viene usata la funzione sendSocketNotiﬁcation(notiﬁcation, payload),

mentre la ricezione viene gestita con la funzione socketNotiﬁcationRe-

ceived(notiﬁcation, payload). I campi di queste due funzioni sono gli

stessi descritti nel punto precedente.

21





Capitolo 4

Applicazioni per il MM

In questo capitolo vengono spiegati i requisiti dei moduli sviluppati durante

lo stage e la loro implementazione. In particolare verranno esposte le dipen-

denze per il modulo dei comandi vocali (sezione [4.1.2),](#br26)[ ](#br26)le metodologie per

accedere ai sevizi di Google (sezione [4.1.2),](#br26)[ ](#br26)come avviene la comunicazione

tra i servizi Google e il programma (sezione [4.1.1)](#br24)[ ](#br24)e l’implementazione del

modulo con Touch Board (sezione [4.2).](#br26)

4.1 Modulo per comandi vocali

La prima applicazione implementata, `e stata il controllo del MM tramite

comandi vocali. Nello speciﬁco l’applicazione deve, tramite delle opportune

frasi, gestire le altre applicazioni presenti nel MM, sfruttando funzioni oﬀerte

dallo stesso.

Nella ﬁgura [4.1](#br24)[ ](#br24)`e rappresentata la struttura e il funzionamento del modulo.

Il microfono cattura l’audio, che viene elaborato, all’interno del NodeHelper,

dal componente ”Elaborazione Audio”. Successivamente, l’audio cos`ı ela-

borato, viene passato all’API Google Speech, la quale lo inoltra al Servizio

Google Speech e si mette in attesa di una risposta. Al ritorno di questa, viene

passata al modulo che ha il compito di validare il comando e di inoltrarlo

in broadcast a tutti i moduli, se corretto. La validazione del comando `e un

semplice controllo di stringa tra il comando ricevuto dal NodeHelper e una

lista di stringhe in un array che corrispondono alla lista di comandi. Alcuni

comandi di esempio sono: mostra ora, per mostrare l’ora, che giorno `e?, per

mostrare il calendario, oppure mostra -nome modulo-, per visualizzare uno

speciﬁco modulo.

Per poter utilizzare l’API `e stato necessario scaricare un software per l’ela-

borazione dell’audio, e, tra le diverse possibilit`a, `e stato scelto il software

22





Sound eXchange (SoX ).

Inoltre `e richiesta un’autenticazione per poter usufruire dei servizi Google.

Figura 4.1: Struttura del modulo per comandi vocali

4.1.1 Comunicazione con l’API di Google

Il NodeHelper dell’applicazione si occupa di gestire lo streaming con l’API e

di mandare i risultati (o gli errori) all’applicazione tramite i metodi di Soc-

ketClient messi a disposizione dal MM, esposte nella sezione [3.4.](#br22)[ ](#br22)Il seguente

codice viene usato per creare un canale streaming con l’API:

1

const recognizeStream = speech . streamingRecognize

( request )

2

3

4

. on( ’ error ’ , sendSocketNotification ( ” error ” ) )

. on( ’ data ’ , ( data ) =>

i f ( Transcription : ${data . r e s u l t s [ 0 ] .

a l t e r n a t i v e s [ 0 ] . t r a n s c r i p t })

sendSocketNotification ( ’ limit reached ’ )

else

5

6

7

sendSocketNotification ( ’ response ’ , data .

r e s u l t s [ 0 ] )

Listing 4.1: Codice per l’inoltro dell’audio al Servizio Google

23





speech.streamingRecognize(request), richiama la funzione dell’API per aprire

una connessione, dove request `e il ﬂusso audio. La funzione si mette suc-

cessivamente in attesa di una risposta dall’API la quale puo` essere di due

tipi:

• errore, nel caso ci sia stato un errore di connessione. In questo caso

viene mandato al modulo un messaggio di errore

• dati di risposta, nel caso di risposta senza errori, ma che pu`o essere

divisa ulteriormente in altre due risposte. La prima sia ha nel caso in

cui viene raggiunto il limite di parole tradotte (Google mette a dispo-

sizione un limite giornaliero per chi vuole usufruirne gratuitamente).

In questo caso il modulo lo notiﬁcherebbe a video con un messaggio di

errore. La seconda risposta contiene una stringa con la frase tradotta,

che il modulo validerebbe come comando, e, in caso di risposta positiva,

la inoltrerebbe ai moduli.

Per passare il ﬂusso audio alla funzione appena descritta bisogna creare una

pipe, ovvero un meccanismo di Comunicazione tra due processi tramite il

quale l’output del primo processo `e inoltrato come input al secondo processo.

Nel seguente codice:

1

// Start recording and send the microphone input

to the Speech API

record

2

3

4

5

6

. s t a r t ({

sampleRateHertz : 1600 ,

threshold : 0 ,

verbose : false ,

7

8

recordProgram : ’ sox ’ ,

s i l e n c e : ’ 20.0 ’

9

10

11

})

. on( ’ error ’ , sendSocketNotification ( ’ error ’ ) )

. pipe ( recognizeStream ) ;

record `e una funzione oggetto con ascolto di eventi che imposta tramite il

metodo .start i settaggi dello streaming (per esempio la frequenza) e ne inizia

la cattura. L’evento .on(’error’) serve per sollevare un’eccezione in caso di

errore, che poi viene inoltrata al modulo. L’evento .pipe(recognizeStream)

crea una pipe tra la funzione di registrazione e recognizeStream descritta nel

codice precedente, passando il ﬂusso audio direttamente alla funzione.

24





4.1.2 Diﬃcolt`a incontrate

Sound eXchange (SoX)

Come discusso nella sezione [4.1,](#br23)[ ](#br23)per permettere all’audio di venire corret-

tamente elaborato per lo streaming, `e necessario utilizzare SoX. Aﬃnch`e

il microfono si colleghi correttamente al programma `e necessario impostare

correttamente i valori delle variabili d’ambiente AUDIODEV e AUDIODRI-

VER. La prima variabile corrisponde al dispositivo audio al quale il program-

ma deve fare riferimento, la seconda variabile al driver audio da utilizzare;

di solito il predeﬁnito `e Advanced Linux Sound Architecture(ALSA).

Autenticazione Google API

Per poter usufruire delle API di Google `e necessario fornire un’autenticazio-

ne a livello di sistema. Per poterlo fare bisogna ottenere delle credenziali di

sicurezza per un account Google, attivabili tramite Google Cloud Platform

Console. Le credenziali consistono in un username, l’email dell’account Goo-

gle e una chiave di sicurezza unica, il tutto contenuto in un ﬁle JSON che pu`o

essere scaricato e salvato in locale. Per permettere al sistema di utilizzare

l’API, occorre che il ﬁle JSON, con le credenziali salvate, sia raggiungibile

all’interno del sistema e per rendere possibile ci`o, bisogna creare una variabi-

le d’ambiente con il nome GOOGLE APPLICATION CREDENTIALS nel

quale viene salvato il percorso dove si trova il ﬁle.

4.2 Modulo con Touch Board

Nell’implementazione del modulo con la Touch Board `e necessario aver in-

stallato nel sistema il linguaggio di programmazione Python, descritto nella

sezione [2.3.10.](#br15)

La Touch Board si presenta come una scheda con 40 porte I/O (le quali de-

vono essere collegate alle GPIO della scheda RaspberryPi) e con un sensore

elettrico di prossimita`, come mostrato in ﬁgura [4.2,](#br27)[ ](#br27)che permette di catturare

i movimenti ﬁno a 5 cm di distanza. Le librerie Python, in dotazione con

la scheda, oﬀrono funzioni per catturare i diversi input trasmessi, come ad

esempio la direzione di spostamento del dito, oppure la cattura di un tocco

sulla scheda.

La struttura del modulo, mostrata in ﬁgura [4.3,](#br28)[ ](#br28)`e composta da un’entita`

Riconoscimento del comando che, al ricevimento di un input sulla Touch

Board, elabora e riconosce il segnale ricevuto (che puo` essere la direzione di

spostamento del dito sulla scheda oppure un tocco) e lo inoltra al modulo.

25





Il comando viene validato dall’entit`a validatore di comando tramite semplice

comparazione tra la stringa ricevuta e un array di stringhe, dove ogni ele-

mento corrisponde ad un possibile comando che si puo` impartire. In caso di

risposta positiva, il comando viene inoltrato in broadcast agli altri moduli,

con i metodi discussi nella sezione [3.4.](#br22)

Per poter eseguire un programma Python sul MM `e necessario usare la libre-

ria Javascript Python-Shell, la quale permette di avviare una shell di Python

in background e avviare, di conseguenza, i programmi. La comunicazione

tra programma Python e il NodeHelper avviene tramite messaggi in JSON.

Quando la scheda riceve un input, il programma Python comunica il risultato

al NodeHelper che lo inoltra al modulo.

Figura 4.2: Touch Board Skydriver by Piromoni

26





Figura 4.3: Struttura del modulo con la Touch Board

27





Capitolo 5

Interfaccia web di

conﬁgurazione

In questo capitolo vengono esposti la progettazione e l’implementazione del-

l’interfaccia web di conﬁgurazione nel MM. Al ﬁne di ospitare la pagina web

che contiene il pannello di conﬁgurazione, `e necessario creare una nuova clas-

se server oltre a quella gia` esistente, citata nel sezione [3.1.](#br18)[ ](#br18)Il server gira su

una porta diﬀerente rispetto al primo server, la quale indicata nel ﬁle di

conﬁgurazione del MM, ed `e accessibile da qualsiasi utente all’interno della

sottorete. La struttura del server viene gestita con Express, spiegato nella

sezione [2.3.6,](#br14)[ ](#br14)che oﬀre funzioni per gestire piu` facilmente le richieste delle

pagine e le relative risposte. Inoltre, all’inizializzazione del server, viene pas-

sato come parametro il ﬁle di conﬁgurazione del MM.

Aﬃnch`e l’interfaccia funzioni completamente `e stato necessario inserire una

nuova dipendenza: per ogni modulo deve essere creato un ﬁle JSON con lo

stesso nome, contenente i campi e le variabili della propria conﬁgurazione.

In particolare, nel capitolo, verranno esposte la struttura del funzionamento

dell’interfaccia (sezione [5.1)](#br29)[ ](#br29)e le metodologie per l’individuazione dei moduli

presenti nel MM, con i relativi ﬁle JSON, al ﬁne di renderli modiﬁcabili (se-

zione [5.2).](#br30)

5.1 Struttura dell’interfaccia Web di conﬁgu-

razione

Dato che il server `e implementato con Express, la struttura `e caratterizzata

dalle due entita` (Controller e Modello), descritte nella sezione [2.3.6.](#br14)[ ](#br14)Come

28





mostrato in ﬁgura [5.1,](#br30)[ ](#br30)un utente (tramite il browser) fa richiesta di una pagi-

na di un determinato modulo passando un Uniform Resource Identiﬁer(URI ),

che viene ricevuto dal controller principale (passo 1) e inoltrato al modello

(passo 2) a cui fa riferimento (in questo caso il modello `e uno soltanto). Il

modello ricerca in locale il ﬁle JSON del modulo richiesto (passo 3) e lo passa

al controller (passo 4 e 5), il quale lo inoltra alla vista. Quest’ultima aggior-

na il template della pagina inserendo i dati contenuti nel JSON che `e stato

passato, e la inoltra al browser che ne ha fatto richiesta.

Non `e stato necessario utilizzare il Routing dal momento che `e stato neces-

sario implementare un solo modello e, di conseguenza, un solo controller.

Figura 5.1: Struttura del server dell’interfaccia web

5.2 Individuazione e visualizzazione dei mo-

duli nell’interfaccia

Come gia` discusso nella sezione [3.3,](#br21)[ ](#br21)tutti i moduli sono contenuti nella car-

tella Modules del MM. Il server, tramite una funzione della libreria, legge i

nomi di tutte le cartelle contenute all’interno di Modules, il cui percorso `e

29





stato passato come parametro alla funzione. In seguito, salva tutti i nomi

dei moduli in una lista, ﬁltrando i ﬁle e le cartelle che non si riferiscono ad

essi. La funzione per leggere le directory, appena citata, oﬀre un metodo per

leggere ed elencare le cartelle in modo sincrono, cos`ı da non rendere necessa-

rio l’utilizzo di callback.

All’interno di Modules `e presente una cartella default, che contiene i moduli

standard in dotazione con il MM. Per poter elencare anche questi ultimi `e

stato necessario utilizzare la funzione di libreria precedentemente usata an-

che su quest’ultima cartella e concatenare, successivamente, le due liste, per

ottenere un’unica lista con tutti i moduli, necessaria per poter popolare il

menu` del pannello web di conﬁgurazione.

Tutte le pagine web che ritorna il server sono divise in 2 sezioni come illustrato

nella ﬁgura [5.2:](#br32)

• Il menu` laterale, che contiene tutti i moduli messi nella lista (ad esempio

calendar e clock). Ogni opzione del menu` corrisponde ad un modulo,

che inoltra la richiesta con il rispettivo URI

• Le varie impostazioni del modulo, visualizzate tramite CodeMirror[\[18\],](#br35)

una componente Javascript che permette l’implementazione di un’area

di testo per la modiﬁca di codici all’interno di una pagina web.

Una pagina web consiste in un ﬁle con estensione mustache contenente co-

dici HTML e variabili Mustache, motore di template esposto nella sezione

[2.3.7.](#br14)[ ](#br14)Il server, alla richiesta di una pagina di uno speciﬁco modulo, ricerca

il relativo ﬁle JSON all’interno della cartella del modulo stesso e lo passa

come parametro sottoforma di oggetto JSON alla funzione render, necessaria

per la creazione e visualizzazione della pagina. Insieme vengono passati i

parametri posizione ed header, trattati nella sezione [3.2.1,](#br20)[ ](#br20)estratti dal ﬁle

di conﬁgurazione passato all’inizializzazione del server. Durante la creazione

della pagina, i vari campi trasmessi, vengono inseriti dentro l’area di testo

di CodeMirror, che permetter`a di eseguirne le modiﬁche. Sotto all’area di

testo `e presente un bottone, che permette di attivare o disattivare il modulo

nel MM; tuttavia aﬃnch`e la modiﬁca venga apportata `e richiesto un riavvio

manuale del software. Le modiﬁche eﬀettuate vengono spedite al server che si

occupa di salvarle nel ﬁle di conﬁgurazione principale del MM. Le metodolo-

gie e le pratiche per modiﬁcare e salvare le modiﬁche nel ﬁle di conﬁgurazione

sono state sviluppate ed implementate da una mia collega.

Nel caso che durante una delle operazioni di fetch o di invio dei dati alla pa-

gina si veriﬁchi un errore, viene mostrata una pagina con un errore generico.

30





Invece, in caso di errata sintassi del ﬁle JSON modiﬁcato, viene ricaricata la

pagina del modulo appena modiﬁcato mostrando una stringa di errore sopra

all’area di editor di testo.

Figura 5.2: Interfaccia web di amminsitrazione

31





Conclusione

Per riassumere il lavoro svolto, si ricorda che durante la prima parte dello

stage sono state sviluppate due interfacce utente per il MM:

• Una vocale, che permette l’impartizione di comandi vocali validi. In

questa parte si `e dovuto aﬀrontare il problema di interfacciarsi ai ser-

vizi Google e di far comunicare correttamente il microfono con le API

esposte, tramite il software SoX

• Una touch, che permette l’impartizione di comandi validi tramite il

movimento delle dita su una scheda touch. Il problema riscontrato

con questa interfaccia `e stato implementare un canale di comunicazio-

ne tra il programma python che cattura i controlli sulla scheda e il

NodeHelper.

Nella seconda parte `e stata implementata un’interfaccia web di conﬁgurazione

remota che permette di conﬁgurare piu` facilmente il MM e i suoi moduli. I

problemi riscontrati in questa parte sono stati:

• La corretta individuazione, visualizzazione e modiﬁca dei ﬁle JSON dei

moduli, contenuti all’interno dei ﬁle locali del MM

• L’utilizzo di una buona pratica di programmazione in Javascript per

evitare fenomeni che portassero ad una scrittura del codice molto con-

fusionaria.

Alcune parti di questi progetti sono ancora arcaici o poco sviluppati: infatti

un possibile sviluppo futuro delle interfacce utente `e l’inserimento di un’unit`a

logica che possa validare i comandi impartiti (sia vocali che touch), in modo

piu` concreto rispetto ad un semplice controllo di stringa.

Invece, per l’interfaccia web di conﬁgurazione, si pu`o implementare un siste-

ma per il riavvio automatico del software, anzich`e farlo manualmente, insieme

ad una crittograﬁa dei messaggi scambiati, in modo da inserire un livello di

sicurezza.

32





Bibliograﬁa

[1] Raspbian wikipedia, <https://it.wikipedia.org/wiki/Raspbian>

[2] Debian wikidia, <https://it.wikipedia.org/wiki/Debian>

[3] Raspberry oﬃcial website, <https://www.raspberrypi.org/>

[4] OpenCV oﬃcial website, <http://opencv.org/>

[5] Google Speech to Text API documentation,

<https://cloud.google.com/speech/>

[6] Electron oﬃcial website, <https://electron.atom.io/>

[7] MVC Wikipedia, [https://en.wikipedia.org/wiki/Model%E2%80%](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)

[93view%E2%80%93controller](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)

[8] Express oﬃcial website, <http://expressjs.com/it/>

[9] MySQL oﬃcial website, <https://www.mysql.com/it/>

[10] Mustache Git Site, <https://mustache.github.io/>

[11] JavaScript, <https://www.javascript.com/>

[12] Python website, <https://www.python.it/>

[13] GitLab website, <https://about.gitlab.com/>

[14] Node.JS website, <https://nodejs.org/it/>

[15] V8 wikipedia,

<https://it.wikipedia.org/wiki/V8_(motore_JavaScript)>

[16] npm docs,

<https://docs.npmjs.com/getting-started/what-is-npm>

[17] Chromium wikipedia, <https://it.wikipedia.org/wiki/Chromium>

33





[18] CodeMirror website, <https://codemirror.net/>

[19] MagicMirror website, <https://magicmirror.builders/>

34


