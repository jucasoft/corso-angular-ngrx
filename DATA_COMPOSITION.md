 - creare 3 nuove sezioni dell'applicazione con i soliti comandi
```
ng generate ngrx-entity-crud:store --name=coin --clazz=Coin --type=CRUD
ng generate ngrx-entity-crud:section --clazz=Coin --lib=primeng
ng generate ngrx-entity-crud:store --name=person --clazz=Person --type=CRUD
ng generate ngrx-entity-crud:section --clazz=Person --lib=primeng
ng generate ngrx-entity-crud:store --name=car --clazz=Car --type=CRUD
ng generate ngrx-entity-crud:section --clazz=Car --lib=primeng
ng generate ngrx-entity-crud:store --name=structure --clazz=Structure --type=CRUD
ng generate ngrx-entity-crud:section --clazz=Structure --lib=primeng
```
 - aggiungere le i dati per le nuove sezioni nel db.json
 - aggiungere le tre sezioni nel menu
 - creare la gestione dell'autenticazione () 




