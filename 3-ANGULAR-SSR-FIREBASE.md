Aggiunta del database

1. Accedi a [Firebase Console](https://firebase.google.com/), cliccando su "Go to console".
2. Seleziona il tuo progetto.
3. Nella barra laterale sinistra, espandi la sezione "Creazione/Sviluppo".
4. Clicca su "Firestore Database".
5. Verrai indirizzato a una pagina introduttiva del prodotto.
6. Clicca su "Crea database".
7. Comparirà una finestra di configurazione:
   - Il campo "ID database" potrebbe non essere modificabile a causa del piano gratuito.
   - Per la località, seleziona "eur3", ottima scelta per utenti europei.
8. Clicca su "Avanti".
9. Seleziona "Avvia in modalità produzione".
10. Clicca su "Crea".
11. Una volta completata la creazione, verrai indirizzato alla pagina di gestione del database. Le regole predefinite non consentono operazioni sul database e devono essere aggiornate.

Gestione delle Regole di Accesso

1. Dal menu di sinistra del progetto, clicca su "Firestore Database".
2. Nella parte superiore della pagina, clicca su "Regole".
3. Troverai la regola predefinita:
```
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false; // La condizione if false impedisce qualsiasi tipo di operazione.
    }
  }
}
```
4. Nota che la condizione "if false" impedisce qualsiasi tipo di operazione.
5. Sostituisci la regola con una più permissiva che consenta operazioni da utenti registrati:
```
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```
6. Clicca su "Pubblica".

Creazione della Pagina per l'Invio dei Dati al Database

1. Apri il codice sorgente del progetto Angular.
2. Apri il file `db.component.ts`.
3. Incolla il seguente codice:
```typescript
import { Component } from '@angular/core';
import { addDoc, collection, Firestore, getDocs } from "@angular/fire/firestore";
import { RouterLink } from "@angular/router";

@Component({
  selector: 'app-db',
  template: `
    <p>
      db works!
    </p>
    <button (click)="add()">add</button>
    <button (click)="getList()">get list</button>
  `,
})
export default class DbComponent {

  constructor(private _fireStore: Firestore) {
    this.add();
  }

  async getList() {
    const querySnapshot = await getDocs(collection(this._fireStore, "users"));
    querySnapshot.forEach((doc) => {
      console.log(doc.id, doc.data());
    });
  }

  async add() {
    try {
      const docRef = await addDoc(collection(this._fireStore, "users"), {
        first: "Bella",
        last: "Zio",
        value: Math.round(Math.random()*99)
      });
      console.log("Document written with ID: ", docRef.id);
    } catch (e) {
      console.error("Error adding document: ", e);
    }
  }
}
```
4. Esegui una build locale per verificare eventuali errori.
5. Fai commit e push delle modifiche.
6. Controlla le azioni su GitHub per assicurarti che terminino correttamente.
7. Dopo qualche secondo, apri il dominio del tuo sito pubblicato.
8. Fai clic sul pulsante "db" dopo esserti autenticato.
9. Clicca diverse volte sul pulsante "add".
10. Clicca su "get list".
11. Apri la console di Chrome e osserva il risultato della lista caricata dal database.
12. Torna alla pagina amministrativa di "Firestore Database". Se tutto è corretto, dovresti vedere i nuovi dati caricati nel database.
