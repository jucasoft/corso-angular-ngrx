# AUTH 
integrazione autenticazione/ngrx
## prerequisiti
 - ngrx-entity-crud >= 11.3.0
 - prima di cominciare con la procedura, committare tutto, in modo da poter revertare in caso di errori.
## procedura
lanciare il comenado `ng generate ngrx-entity-crud:auth`
verranno generati i seguenti file:
```
CREATE src/app/main/views/login/login-routing.module.ts (546 bytes)
CREATE src/app/main/views/login/login.module.ts (819 bytes)
CREATE src/app/main/views/login/components/logout-button/logout-button.component.ts (1158 bytes)
CREATE src/app/main/views/login/login-main/login-main.component.html (1074 bytes)
CREATE src/app/main/views/login/login-main/login-main.component.ts (1590 bytes)
CREATE src/app/root-store/auth-store/actions.ts (1148 bytes)
CREATE src/app/root-store/auth-store/auth-mock.service.ts (2039 bytes)
CREATE src/app/root-store/auth-store/auth-store.module.ts (1017 bytes)
CREATE src/app/root-store/auth-store/auth.guard.ts (1359 bytes)
CREATE src/app/root-store/auth-store/auth.service.ts (731 bytes)
CREATE src/app/root-store/auth-store/conf.ts (76 bytes)
CREATE src/app/root-store/auth-store/effects.ts (1340 bytes)
CREATE src/app/root-store/auth-store/index.d.ts (271 bytes)
CREATE src/app/root-store/auth-store/index.ts (271 bytes)
CREATE src/app/root-store/auth-store/names.ts (47 bytes)
CREATE src/app/root-store/auth-store/reducer.ts (731 bytes)
CREATE src/app/root-store/auth-store/selectors.ts (1525 bytes)
CREATE src/app/root-store/auth-store/state.ts (313 bytes)
CREATE src/app/main/models/vo/auth.ts (277 bytes)
UPDATE src/app/app-routing.module.ts (557 bytes)
UPDATE src/app/root-store/index.ts (309 bytes)
UPDATE src/app/root-store/index.d.ts (309 bytes)
UPDATE src/app/root-store/state.ts (184 bytes)
UPDATE src/app/root-store/root-store.module.ts (1051 bytes)
```
 - riavviare la compilazione per evitare eventuali errori.
 - aprire http://localhost:4200/login/main
 
 ## Test
 ### 1 error messag
 - inserire i seguenti dati:
    - user: aaa
    - password: bbb
 - click su Login
 - esito atteso:
    - appare un messaggio di errore: `user:"aaa" does not exist`

 ### 2 error messag
 - inserire i seguenti dati:
    - user: `cipo`
    - password: `bbb`
 - click su Login
 - esito atteso:
    - appare un messaggio di errore: `error passwd:aaa for user: "cipo"`

 ### 3 login ok
 - inserire i seguenti dati:
    - user: `cipo`
    - password: `cipo`
 - click su Login
 - esito atteso:
    - reindirizzamento su `home`
    
    
## Guard
Guard per bloccare l'accesso a determinate sezioni senza autenticazione:
src/app/root-store/auth-store/auth.guard.ts

## Service
sono presenti due servizi:
```
src/app/root-store/auth-store/auth.service.ts // servizio dove implementare le chiamate remote
src/app/root-store/auth-store/auth-mock.service.ts // servizio con autenticazione moccata
```

## LogoutButton
`logout-button.component.ts` componente per effettuare il logout.

## Autenticazione persistente
per rendere persistente l'autenticazione consiglio di utilizzare: `ngrx-store-localstorage`, che permette di salvare nel localstorage del browser qualsiasi porzione dello store.

