Ciao, in questo post voglio condividere con voi come creare un'applicazione Angular con server-side rendering (SSR) e ospitarla su Firebase usando GitHub Actions. Questo è un modo semplice e veloce per avere un sito web performante e scalabile, sfruttando i vantaggi del SSR e del cloud.

Per seguire questo tutorial, avrete bisogno di:

- Account GitHub
- Account Firebase
- Node.js v18.18.2 e npm v10.2.4
- Il pacchetto firebase-tools@13.1.0 installato globalmente
	`npm i -g firebase-tools`
- Il pacchetto @angular/cli@17.1.2 installato globalmente
	`npm i -g @angular/cli`

Ecco i passi da seguire:

1. Crea e loggati in:
 https://github.com/
 https://firebase.google.com/

2. Crea un nuovo progetto Angular con SSR:
ng new ng17-ssr-firebase -s -t -S --ssr --style=scss

3. Entra nella cartella del progetto:
cd ng17-ssr-firebase

4. Crea un nuovo repository PRIVATO su GitHub con lo stesso nome del progetto
5. Segui le istruzioni che appaiono su GitHub per associare il tuo progetto locale, sotto la sezione "…or push an existing repository from the command line" del tipo:
	git remote add origin https://github.com/{{user}}/ng17-ssr-firebase.git
	git branch -M main
	git push -u origin main

6. Inizializza il progetto Firebase (da dentro la cartella del progetto Angular, necessario installare `npm i -g @angular/cli`)
firebase init

7. Rispondi alle domande che ti vengono poste:

? Are you ready to proceed?
	Yes

? Which Firebase features do you want to set up for this directory?
	Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys

? Please select an option:
	Create a new project
	
? What do you want to use as your public directory? public
? Configure as a single-page app (rewrite all urls to /index.html)? Yes
? Set up automatic builds and deploys with GitHub? Yes
+  Wrote public/index.html

8. Accedi a GitHub quando ti viene richiesto, aprendo il browser
9. Inserisci il nome del tuo repository rispondendo alla domanda:
- For which GitHub repository would you like to set up a GitHub workflow? (format: user/repository)
in pratica devi fare copia incolla dell'URL del tuo repository GitHub
10. Conferma la creazione della workflow file e delle secret keys

A questo punto, hai configurato il tuo progetto per essere ospitato su Firebase e per essere deployato automaticamente ogni volta che fai una modifica al codice e la pushi su GitHub.

Testiamo il funzionamento.
Prima però ti consiglio di aprire il repository Github che hai creato, nella parte superiore clicca su "action", per ora non vedrai nulla ma ti sarà utile averla già aperta

ora poi fare:

git add .
git commit -m "test deploy"
git push

Riapri la pagina Github delle action e aggiornala, vedrai partire il processo di build che pubblicherà in automatico il file public/index.html 

Aspetta qualche minuto che la workflow si completi, 
poi apri https://firebase.google.com/
se necessario fai log-in
clicca in alto a destra su "Go to console"
clicca sul pulsantone rettangolare con il nome del tuo progetto 
dal menu di sinistra clicca su "hosting"
nel riquadro "Domini" troverai i due link per aprire il sito
se ti appare una pagina con scritto "Welcome Firebase Hosting Setup Complete" sta funzionando
Per testare il funzionamento, puoi modificare il file public/index.html con il testo che preferisci,
torna sul temrinale ed esegui:
git commit -m "test deploy B"
git push

nella pagina delle action di GitHub vedrai partire nuovamente la build.
dopo aver terminato apri nuovamente il tuo dominio di firebase

Congratulazioni, hai creato la tua applicazione Angular con SSR e l'hai ospitata su Firebase!

Peccato che non stai realmente pubblicando il compilato di Angular, ma sei a pochissima strada dal riuscirci.

Nelle prossime puntate:
pubblichiamo il compilato di angular
aggiungiamo le librerie js per firebase
Abilitiamo l'autenticazione con il provider Google
Eseguiamo il login da Angular con il provider di Google
aggiungiamo un db e modifichiamo le regole di accesso, solo gli utenti loggati potranno scrivere in una loro sezione
Caricheremo dati da Angular (solo se autenticati)
aggiungiamo uno storage e modifichiamo le regole di accesso, solo gli utenti loggati potranno scrivere in una loro sezione
Caricheremo delle immagini da Angular (solo se autenticati)
