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

##descrizione plugin

####(*) TypeScript (required by other typescript plugins)

	https://www.graphql-code-generator.com/docs/plugins/typescript

Questo plugin genera i tipi TypeScript di base, in base al tuo schema GraphQL.
I tipi generati da questo plugin sono semplici e si riferiscono alla struttura esatta
del tuo schema, ed è usato come tipi di base per altri plugin
(come typescript-operations/ typescript-resolvers)

####(*) TypeScript Operations (operations and fragments)

	https://www.graphql-code-generator.com/docs/plugins/typescript-operations

Questo plugin genera tipi TypeScript in base al tuo GraphQLSchema e alle tue operazioni e frammenti GraphQL.
Genera tipi per i tuoi documenti GraphQL: Query, Mutation, Subscription e Fragment.

Nota: nella maggior parte delle configurazioni, questo plugin richiede anche
l'uso di `typescript, perché dipende dai suoi tipi di base.

####(*) TypeScript Apollo Angular (typed GQL services) <========== installa in automatico una versione di apollo angular comptibile

	https://www.graphql-code-generator.com/docs/plugins/typescript-apollo-angular

Questo plugin genera servizi Apollo ( Query, Mutatione Subscription) con digitazioni TypeScript.

Genererà un servizio Angular fortemente tipizzato per ogni query, mutazione o
sottoscrizione definita. I servizi Angular generati sono pronti per essere
iniettati e utilizzati all'interno del tuo componente Angular.

Estende i plugin TypeScript di base: @graphql-codegen/typescript,
@graphql-codegen/typescript-operations-
e quindi condivide una configurazione simile.

####( ) TypeScript GraphQL files modules (declarations for .graphql files)

	https://www.graphql-code-generator.com/docs/generated-config/typescript-graphql-files-modules

Questo plugin genera digitazioni TypeScript per file .graphql contenenti documenti GraphQL,
che in seguito possono essere consumati utilizzando graphql-tag/loadero utilizzare i
tipi string se utilizzerai le operazioni come stringhe non elaborate e otterrai il
controllo del tipo e la sicurezza del tipo per le tue importazioni. Ciò significa
che ogni volta che importi oggetti da file .graphql, il tuo IDE fornirà il completamento
automatico.

Questo plugin gestisce anche file .graphql contenenti più documenti GraphQL e nomina le
importazioni in base al nome dell'operazione.

####( ) TypeScript GraphQL document nodes (embedded GraphQL document)

	https://www.graphql-code-generator.com/docs/plugins/typescript-document-nodes

Questo plugin genera il file .ts sorgente TypeScript ( ) dai file GraphQL ( .graphql).

####( ) Introspection Fragment Matcher (for Apollo Client)

	https://www.graphql-code-generator.com/docs/plugins/fragment-matcher

Questo plugin genera un file di introspezione ma solo con interfacce e unioni, in base al tuo GraphQLSchema.

Se stai utilizzando apollo-cliente il tuo schema contiene interfaceo una uniondichiarazione, si consiglia di
utilizzare Fragment Matcher di Apollo e il risultato generato dal plugin.

Puoi leggere di più a riguardo nella apollo-clientdocumentazione:
https://www.apollographql.com/docs/react/data/fragments/#fragments-on-unions-and-interfaces .

Il plug-in Fragment Matcher accetta un file TypeScript/JavaScript o JSON come output ( .ts, .tsx, .js, .jsx, .json) .

Sia in TypeScript che in JavaScript viene utilizzata un'esportazione predefinita.

####( ) Urql Introspection (for Urql Client)

	https://www.graphql-code-generator.com/docs/plugins/urql-introspection

Questo plugin genera un file di introspezione per la funzione Schema Awareness di Urql Cache Exchange

Puoi leggere di più a riguardo nella urqldocumentazione: https://formidable.com/open-source/urql/docs/graphcache/schema-awareness/ .

Il plug-in Urql Introspection accetta un file TypeScript/JavaScript o JSON come output ( .ts, .tsx, .js, .jsx, .json) .

Sia in TypeScript che in JavaScript viene utilizzata un'esportazione predefinita.


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
