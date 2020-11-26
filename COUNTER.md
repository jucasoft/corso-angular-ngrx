# [TUTORIAL ngrx/store counter](https://ngrx.io/guide/store#tutorial) 
Per prima cosa eseguire il [TUTORIAL counter](https://ngrx.io/guide/store#tutorial) di NGRX, 
!!attenzione, nel punto 1 del tutorial, cliccando su "live example" si apre stackblitz.com, in questa pagina prima di iniziare lo sviluppo dovete cliccare sul pulsante blu "Fork".

Dopo aver finito il tutorial online, proviamo ad implementare la medesima funzionalita` sul nostro pc locale.
Prerequisito: creare l'applicaizone seguendo il tutorial [ngrx-entity-crud](https://www.npmjs.com/package/ngrx-entity-crud)

- crea uno store di tipo BASE, senza la gestione CRUD
```
ng generate ngrx-entity-crud:store --name=counter --clazz=Counter --type=BASE
```

- crea una nuova sezione grafica dell'applicaizone
```
ng generate ngrx-entity-crud:section --clazz=Counter --lib=no-libs
```

