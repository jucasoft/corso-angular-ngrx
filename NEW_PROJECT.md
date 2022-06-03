```

ng new ng13b --routing true --style scss
cd ng13b
npm i @angular/cdk 
npm i @ngrx/store 
npm i @ngrx/entity 
npm i @ngrx/effects 
npm i @ngrx/store-devtools 
npm i @ngrx/router-store 
npm i primeng 
npm i primeicons 
ng add ngrx-entity-crud

angular.json:
"styles": [
"node_modules/primeicons/primeicons.css",
"node_modules/primeng/resources/themes/lara-light-blue/theme.css",
"node_modules/primeng/resources/primeng.min.css",
"src/styles.scss"
],


ng generate ngrx-entity-crud:store --name=crud-plural --clazz=CrudPlural --type=CRUD-PLURAL

tsconfig.json:
"strict": false,
"noImplicitOverride": false,
"noPropertyAccessFromIndexSignature": false,
"noImplicitReturns": false,

	add:
	+ "allowSyntheticDefaultImports": true

environment.ts:
+ webServiceUri:""

```
