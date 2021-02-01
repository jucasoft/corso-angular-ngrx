# Ambiente di sviluppo
Preparare ambiante di sviluppo senza di diritti amministrativi.

## 1 GIT
- aprire la pagina per il download https://git-scm.com/download/win
- scaricare la versione "64-bit Git for Windows Portable"
- eseguire il file scaricato
- selezionare come cartella di installazione "C:\DEV\kit\git" 
- NOTE: in realtà non si tratta di una "installazione", git viene solo decompresso, non necessita diritti admin
   
## 2 nodejs
- aprire la pagina nodejs.org
- in corrispondenza della versione LTS, click su Other Download
- scaricare la versione "Windows Binary (.zip)" a 64bit
- decomprimere il file .zip in C:\DEV\kit\node\
- verificare che sia presente il file "C:\DEV\kit\node\node.exe"
- aprire CDM, aggiungere la variabile ambiente con il comando "set path=%path%C:\DEV\kit\node", questa variabile ambiente non e` persistente, devi reimpostarla al successivo riavvio di CMD (se doveste avere i diritti amministrativi, settatela in modo persistente)
- digitare "npm -v" + invio, per verificare il funzionamento di npm
- digitare "node -v" + invio, per verificare il funzionamento di node
- digitare "npm i -g @angular/cli", per installare angular/cli, se dovessero apparire scelte y/n, fate voi.
- digitare "ng version", per verificare il funzionamento di angular/cli
- senza chiudere CMD creiamo il nostro primo progetto Angular
- posizionarsi in una cartella a scelta
- lanciare il comando "ng new testA"
- selezionare risposte casuali per eventuali scelte
- entrate nella cartella del programma appena creato "cd testA"
- digitare il comando "npm run start"
- ecco pronta la prima applicazione Angular su localhost:4200
   
## 3 IntelliJ IDEA Ultimate
- creare sul proprio pc la cartella C:\DEV\programs\intellij
- andare sulla pagina web per il download di IntelliJ IDEA Ultimate
- scaricare la versione .zip del programma, nella cartella precedentemente creata
- tasto destro sullo zip, selezionare "estrai tutto"
- verificare la presenza del file "C:\DEV\programs\intellij\ideaIU-xxxxxxx\bin\idea64.exe"
- doppio click su "idea64.exe"   

### 3.1 Schermate primo avvio:
- Accettare i termini e prosegui.
- Data Sharing, libero di scegliere
- Pagina licenza, selezionare "Evaluate for free" + click su "Evaluate"
- A questo punto le schermate variano in base alla versione scaricata:
    - stile grafico, a me piace quello scuro
    - plugin, potete lasciare tutto predefinito
	   	
	   	
### 3.2 CONFIGURAZIONE:
- all'apertura di intellij appare la finestra "Welcome IntelliJ IDEA" 

#### 3.2.1 configurare git:
- aprire command prompt, digitatare "git -v", in caso di non riconoscimento del comando settare la variabile d'ambiente di git, il path sarà "C:\DEV\kit\git\bin"

#### 3.2.2 configurare nodejs
- aprire command prompt, digitatare "node -v" e successivamente "npm -v" in caso di non riconoscimento dei comandi settare la variabile d'ambiente di node "C:\DEV\kit\node"

   
   
