ng new ng13
npm i @angular/cdk
npm i @ngrx/store @ngrx/entity @ngrx/effects @ngrx/store-devtools @ngrx/router-store
npm i primeng primeicons
npm i @angular/cdk @ngrx/store @ngrx/entity @ngrx/effects @ngrx/store-devtools @ngrx/router-store primeng primeicons ngrx-entity-crud@beta
npm i ngrx-entity-crud@beta


angular.json:
"styles": [
"node_modules/primeicons/primeicons.css",
"node_modules/primeng/resources/themes/lara-light-blue/theme.css",
"node_modules/primeng/resources/primeng.min.css",
"src/styles.scss"
],

ng generate ngrx-entity-crud:ng-add

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
