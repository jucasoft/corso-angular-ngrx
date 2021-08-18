# libreria per la gestione delle dipendenze, 
da valutare se necessaria. veramente interessante.
https://ngrx-entity-relationship.sudo.eu/

# (tutorial) graphql-code-generator
nuovo progetto angular
ng new testGQL

installare serverino json-graphql-server:https://github.com/marmelab/json-graphql-server
installare libreria
creare file db.js
aggiungere script  "scripts":
{
"start:glq": "json-graphql-server db.js",
},


istruzionei per installare graphql-code-generator

npm install --save graphql
npm install --save-dev @graphql-codegen/cli
npm i

inizializzare il progetto
npx graphql-codegen init

appaiono una serie di scelte:

? What type of application are you building? Application built with Angular
? Where is your schema?: (path or url) http://localhost:4000 <======= queste impostazioni potranno essere cambiate in un seconod momento
? Where are your operations and fragments?: src/**/*.graphql
? Pick plugins: (Press <space> to select, <a> to toggle all, <i> to invert selection) <======== analizzare con attenzione cosa viene generato attivando i vari plugin
>(*) TypeScript (required by other typescript plugins)
(*) TypeScript Operations (operations and fragments)
(*) TypeScript Apollo Angular (typed GQL services) <========== installa in automatico una versione di apollo angular comptibile
( ) TypeScript GraphQL files modules (declarations for .graphql files)
( ) TypeScript GraphQL document nodes (embedded GraphQL document)
( ) Introspection Fragment Matcher (for Apollo Client)
( ) Urql Introspection (for Urql Client)


nei test eseguiti sul mio pc, il processo di inizializzazione aveva aggiunto in automatico le librerie dei plugin
e bisognava solo lanciare npm i, mentre su altre postazioni bisogna installare le librerie singolarmente
installarli a mano:

npm i -D @graphql-codegen/typescript
npm i -D @graphql-codegen/typescript-operations
npm i -D @graphql-codegen/typescript-apollo-angular
npm i -D @graphql-codegen/introspection

installare e configurare apollo angular:
npm i @apollo/client
npm i apollo-angular

ATTENZIONE!!in caso di errori/conflitti durante l'installazione, aggiungere le librerie a mano nel package.json e lanciare npm i

aggiungere la configurazione nel modulo principale come da guida online e fare attenzione da dove vengono importati i moduli.
```
import {HttpClientModule} from '@angular/common/http';
import {APOLLO_OPTIONS} from 'apollo-angular';
import {HttpLink} from 'apollo-angular/http';
import {InMemoryCache} from '@apollo/client/core'; <<=== intellij importa questo modulo da '@apollo/client' dando parecchi errori.

@NgModule({
  imports: [BrowserModule, HttpClientModule],
  providers: [
    {
      provide: APOLLO_OPTIONS,
      useFactory: (httpLink: HttpLink) => {
        return {
          cache: new InMemoryCache(),
          link: httpLink.create({
            uri: 'https://48p1r2roz4.sse.codesandbox.io', <<== sostituire con percorso corretto
          }),
        };
      },
      deps: [HttpLink],
    },
  ],
})
export class AppModule {}
```

ed aggiuno lo script per la generazione (in alcuni casi viene aggiunto in automatico dallo script di inizializzazione)
```
{
  "scripts": {
    "generate": "graphql-codegen"
  }
}
```

creo il file app.graphql:
```
query allpost{
  allPosts {
    title
    views
  }
}
```

lanciare il comendo "npm run generate"

testare il funzionameto della chiamata, aggiungere a componente app.component.ts:
```
  constructor(private allpostGQL: AllpostGQL) {
    debugger
    allpostGQL.fetch().subscribe(value => console.log('allpostGQL.fetch():' + value));
  }
```
!ATTENZIONE in caso di errore nel codice, verificare che la seguente importazione sia corretta:
```
import {InMemoryCache} from '@apollo/client/core'; <<=== intellij importa questo modulo da '@apollo/client' dando parecchi errori.
```
