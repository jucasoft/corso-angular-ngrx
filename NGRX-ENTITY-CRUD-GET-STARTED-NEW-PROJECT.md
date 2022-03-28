ng new projectName
npm i @ngrx/store @ngrx/entity @ngrx/effects @ngrx/store-devtools @ngrx/router-store
npm install primeng primeicons


angular.json:
"styles": [
"node_modules/primeicons/primeicons.css",
"node_modules/primeng/resources/themes/lara-light-blue/theme.css",
"node_modules/primeng/resources/primeng.min.css",
"src/styles.scss"
],

npm i ngrx-entity-crud@beta
ng generate ngrx-entity-crud:ng-add
[-] le sezioni non possono essere aggiunte, mancano i componenti presenti sotto core.

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
