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
 - aggiungere le tre sezioni nel menu (seguire la guida [SLIDE_MENU](SLIDE_MENU.md))
 - creare la gestione dell'autenticazione (seguire la guida [AUTH](AUTH.md))

esito atteso: profilare le voci di menu in modo che appaiano solo quelle per cui siamo abilitati.
aggiungere l'attributo a tutte le voci di menu per permettere la profilazione:
```
...
// @ts-ignore  
roles: ['roleA'] // <== utilizzando il ruolo 'guest' permette di vedere la voce di menu sempre, anche senza autenticazione.
...
```
aprire il file `src/app/root-store/slide-menu-store/selectors.ts`
creare una nuova select:
```
export const selectItemsAuth: MemoizedSelector<object, MenuItem[]> = createSelector(
  selectItems,
  AuthStoreSelectors.selectRoles,
  (menuItems: MenuItem[], roles) => {
    roles = [roles, 'guest'] ? roles : ['guest'];
    return menuItems.reduce((previous, current) => {
      console.log('reduce.()');
      // @ts-ignore
      if ((current.roles as string[]).find(value => roles.indexOf(value) !== -1)) {
        return [...previous, current];
      }
      return previous;
    }, []);
  }
);
```

modificare il componente `slide-menu.component.ts`
```
...
  ngOnInit(): void {
    this.items$ = this.store$.pipe(
      select(SlideMenuStoreSelectors.selectItemsAuth), // <== cambiamo la select da utilizzare
      menuItemsDecorator(this.store$)
    );  
...
```

