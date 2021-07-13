# HUSKY + LINT-STAGED

integrazione husky + lint-staged

## prerequisiti

- prima di cominciare con la procedura, committare tutto, in modo da poter revertare in caso di errori.

## procedura

-	seguire il tutorial per installare husky a questo link

	https://github.com/typicode/husky

durante il tutorial dovremo sostituire "npm test" con "lint-staged"

Husky ci permetterà di eseguire degli script automatici in determinati casi, nel nostro caso imposteremo uno script per eseguire eslint sui file prima di committare.
Per fare ciò avremo bisogno di lint-staged che ci permetterà di eseguire gli script soltanto per i file da committare

-    installare lint-staged con il seguente comando
```
npm install lint-staged
```

nel package.json verrà creata una sezione "lint-staged", dovremo sostituire i comandi presenti con "eslint --fix" come unico comando da eseguire 

Non rimane che testare il tutto eseguendo un commit.


## possibili errori

- file .git non trovato (durante installazione di husky)

soluzione: individuare il nostro file .git e specificare il path nei comandi del tutorial, esempio:

```
npm install husky -D
 
npm set-script prepare "cd.. && husky install TUO_PATH/.husky"
 
npm run prepare
 
npx husky add TUO_PATH/.husky/pre-commit "cd TUO_PATH  lint-staged"
 
git add TUO_PATH/.husky/pre-commit
 
git commit -m "Keep calm and commit"
```
