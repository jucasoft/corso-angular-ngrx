1. Passiamo a creare una nuova app in FireBase.
2. Apriamo https://firebase.google.com/.
3. Clicchiamo in alto a destra su "Go to console".
4. Clicchiamo sul progetto.
5. Sotto al titolo del progetto, clicchiamo su "+ aggiungi app".
6. Selezioniamo la tipologia "web".
7. Nel campo "Nickname app", consiglio il medesimo nome del progetto più "-web", ad esempio NomeProgetto-web.
8. Selezioniamo la checkbox "inoltre, configura FireBase Hosting per questa app".
9. Nella select sottostante selezioniamo l'host già presente.
10. Clicchiamo sul pulsante "Registra app".
11. Appariranno dei passaggi numerati.
12. Se avete voglia, leggetevi le informazioni al passo 2, ma per ora non fate nulla, vedremo come ritrovare queste informazioni successivamente.
13. Clicchiamo sul pulsante "avanti".
14. Il passaggio 3 non richiede alcuna azione, abbiamo già installato "firebase-tools".
15. Clicchiamo sul pulsante "avanti".
16. Anche per il punto 4, non dobbiamo fare nulla, la Action di Github si occuperà per noi di pubblicare il progetto ad ogni push.
17. Clicchiamo sul pulsante "Vai alla console".
18. A cosa serve una app? Boh! Andrebbe chiesto a qualcuno che ne sa di FireBase. Personalmente, mi ero arenato inizialmente, non capivo dove trovare i dati di configurazione. Infatti, abbiamo creato la app solo per questo motivo: poter avere i dati di configurazione. Ora, sotto al titolo del progetto si trova la nuova app appena creata. Cliccando sul link della nuova appa (presente sotto al titolo del progetto) e successivamente sulla rotella che appare, si potranno recuperare i dati di configurazione.

Torniamo a lavorare sulla app Angular

1. Apriamo il sorgente dell'applicazione Angular precedentemente creata.
2. Eseguiamo una build con `npm run build`.
3. Verifichiamo che sia stato creato il compilato:
   - Per progetti ssr/ssg => `dist/{{nome-progetto}}/browser`
   - Per SPA `dist/{{nome-progetto}}`
4. Apriamo il file `firebase.json` presente nella root del progetto.
5. Aggiorniamo il parametro "public" con il percorso della cartella del compilato. Ad esempio, "dist/ng17-ssr-firebase/browser".
6. Eseguiamo un commit della modifica e un push, verifichiamo che l'azione in GitHub completi correttamente, e apriamo il nostro dominio Firebase.
7. Se sei arrivato fino a questo punto senza problemi è molto strano, fortuna del principiante.

Nelle ultime versioni di Angular hanno deciso di rimuovere le environments, maledetti ignoranti e stolti. Ora dovremmo crearle manualmente e modificare il file `angular.json`, ma non basta lanciare il comando:

```bash
ng g environments
CREATE src/environments/environment.ts (31 bytes)
CREATE src/environments/environment.development.ts (31 bytes)
UPDATE angular.json (3982 bytes)
```

BUUUM! Ora abbiamo le nostre amate variabili d'ambiente ed è stato aggiornato `angular.json`.


1. Apriamo il file appena creato `src\environments\environment.ts`.
2. Dobbiamo aggiungervi la configurazione che possiamo trovare nella app FireBase, ricordi, sotto il nome del progetto hai la app creata all'inizio di questo tutorial.
3. Il contenuto della nostra variabile ambiente deve essere di questo tipo:
```typescript
export const environment = {
  firebaseConfig : {
    apiKey: "..............", // dati finti, con i puntini non potrà funzionare
    authDomain: ".................firebaseapp.com",
    projectId: "....................",
    storageBucket: ".............appspot.com",
    messagingSenderId: ".............",
    appId: "................."
  }
};
```

Inserisci i dati reali trovati nella tua app Firebase al posto dei puntini nell'esempio sopra.

Installaimo altre librerie:
`npm i firebase@latest @angular/fire@latest`

nel momento in cui sto scrivendo questo tutorial ho installato le versioni:
```
    "@angular/fire": "^17.0.1",
    "firebase": "^10.8.0",
```

Ora andremo a configurare in un solo passaggio:

**FirebaseApp**: difficile da spiegare, fa capo alla nostra app creata precedentemente.  
**Firestore**: database di documenti NoSQL.  
**Storage**: Storage di file.  
**Auth**: Autenticazione.

Apriamo il file `app.config.ts` ed incollavi questo codice:

```typescript
import { ApplicationConfig, importProvidersFrom } from '@angular/core';
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';
import { provideClientHydration } from '@angular/platform-browser';
import { initializeApp, provideFirebaseApp } from "@angular/fire/app";
import { environment } from "../environments/environment";
import { getFirestore, provideFirestore } from "@angular/fire/firestore";
import { getStorage, provideStorage } from "@angular/fire/storage";
import { getAuth, provideAuth } from "@angular/fire/auth";

export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter(routes),
    provideClientHydration(),
    importProvidersFrom([
      provideFirebaseApp(() => initializeApp(environment.firebaseConfig)),
      provideFirestore(() => getFirestore()),
      provideStorage(() => getStorage()),
      provideAuth(() => getAuth())
    ])
  ]
};
```

Ora passiamo a modificare `app.component.ts`:

```typescript
import { Component } from '@angular/core';
import { RouterLink, RouterOutlet } from '@angular/router';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [RouterOutlet, RouterLink],
  template: `
    <button routerLink="login/">login</button>
    <button routerLink="upload/">upload</button>
    <button routerLink="home/">home</button>
    <button routerLink="db/">db</button>

    <router-outlet />
  `,
  styles: [],
})
export class AppComponent {
}
```

`app.routes.ts`:

```typescript
import { Routes } from '@angular/router';

export const routes: Routes = [
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  { path: 'home', loadComponent: () => import('./main/views/home/home.component') },
  { path: 'login', loadComponent: () => import('./main/views/login/login.component') },
  { path: 'upload', loadComponent: () => import('./main/views/upload/upload.component') },
  { path: 'db', loadComponent: () => import('./main/views/db/db.component') },
  { path: '**', redirectTo: 'home' } // this needs to be after other routes
];
```

Dalla console posizioniamoci nella root del progetto e creiamo le 4 pagine dell'applicazione:

```
ng g component ./main/views/home
ng g component ./main/views/login
ng g component ./main/views/upload
ng g component ./main/views/db
```

Apriamo il file `home.component.ts` e aggiungiamo "default" tra "export" e "class", il risultato: "`export default class HomeComponent`".

Eseguiamo la stessa operazione sulle altre 3 pagine create.

Prima di procedere, consiglio vivamente di fare una build. Se non ci sono errori, esegui un commit e un push. Dopo che l'azione di Github sarà terminata, apri il tuo dominio Firebase. Se continui a non ricordarti il tuo dominio, ti consiglio di salvarlo tra i preferiti :).

Codice per il file `login.component.ts`:

```typescript
import { Component } from '@angular/core';
import { idToken, user, Auth, signInWithPopup } from "@angular/fire/auth";
import { GoogleAuthProvider } from "firebase/auth";
import { Router } from "@angular/router";
import { AsyncPipe, JsonPipe } from "@angular/common";

@Component({
  selector: 'app-login',
  standalone: true,
  imports: [
    JsonPipe,
    AsyncPipe
  ],
  template: `
    <p>
      login works!
    </p>
    <div>user$: {{user$ | async | json}}</div>
    <div>idToken$: {{idToken$ | async}}</div>
    <button (click)="logout()">Logout</button>
    <button (click)="login()">Login with Google</button>
  `,
  styles: ``
})
export default class LoginComponent {
  redirect = ['/'];
  constructor(private router: Router, private auth: Auth) {
  }
  public user$ = user(this.auth);
  public idToken$ = idToken(this.auth);
  login() {
    const provider = new GoogleAuthProvider();

    signInWithPopup(this.auth, provider).then(value => {
      this.router.navigate(this.redirect);
    });
  }

  logout() {
    this.auth.signOut();
  }

}
```

Commit e push, attendere il tempo necessario per la pubblicazione. Aprire il sito, click su login, click su "Login with Google". ATTENZIONE!! IN CONSOLE DEVE APPARIRVI UN ERRORE.

Non abbiamo ancora configurato nulla in Firebase, dobbiamo aggiungere il sistema di autenticazione. Era necessario testare il sistema in caso di errore :).

Apri il nostro progetto nella console di Firebase:

1. Vai su https://firebase.google.com/.
2. Clicca su "Go to console".
3. Seleziona il tuo progetto.

Nel menu di sinistra, clicca per espandere la sezione "creazione/develop". Clicca su "Authentication". Click su "Inizia". Seleziona come provider "Google". Clicca su abilita. Compila il campo relativo a "Email dell'assistenza per il progetto". Scorri nella parte bassa del form e clicca su "Salva". Abbiamo aggiunto il nostro primo provider.

Torniamo sul nostro sito pubblicato in precedenza. Click su login, click su "Login with Google". Segui le istruzioni della pop-up per eseguire il login. Se il login è andato a buon fine, verremo reindirizzati sulla home, quindi premere nuovamente su login per vedere i dati relativi al login.
