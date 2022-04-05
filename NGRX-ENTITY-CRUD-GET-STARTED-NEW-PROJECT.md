```
ng version
node -v
npm -v
```

```
ng new projectName --routing --style=scss
cd projectName
npm i @ngrx/store @ngrx/entity @ngrx/effects @ngrx/store-devtools @ngrx/router-store
npm i primeng primeicons
npm i ngrx-entity-crud@latest

```

angular.json:
```
"styles": [
"node_modules/primeicons/primeicons.css",
"node_modules/primeng/resources/themes/lara-light-blue/theme.css",
"node_modules/primeng/resources/primeng.min.css",
"src/styles.scss"
],
```

```
ng generate ngrx-entity-crud:ng-add
ng generate ngrx-entity-crud:store --name=crud-plural --clazz=CrudPlural --type=CRUD-PLURAL
```

tsconfig.json:
```
"strict": false,
"noImplicitOverride": false,
"noPropertyAccessFromIndexSignature": false,
"noImplicitReturns": false,
```

add:

	+ "allowSyntheticDefaultImports": true

environment.ts:

	+ webServiceUri:""
