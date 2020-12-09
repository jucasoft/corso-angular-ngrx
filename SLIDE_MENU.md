# SlideMenu
Modifica del menu, per permettere l'apertura delle sezioni create.  
Prerequisito: creare l'applicaizone seguendo il tutorial [ngrx-entity-crud](https://www.npmjs.com/package/ngrx-entity-crud)  
Le voci di menu sono di tipo [MenuModel](https://primefaces.org/primeng/showcase/#/menumodel)

N.B. dalla versione 11.3.0 le voci di menu si trovano nello store, per versioni precedenti dell'appicazione bisogna mergiare i seguenti file:
```
CREATED "src/app/main/components/slide-menu/slide-menu.component.ts"
UPDATE  "src/app/root-store/slide-menu-store/operators.ts"
UPDATE  "src/app/root-store/slide-menu-store/selectors.ts"
UPDATE  "src/app/root-store/slide-menu-store/state.ts"
```

## Aggiungere elementi al SlideMenu
aprire file: "src/app/root-store/slide-menu-store/state.ts"
le voci di menu sono l'attributo `items`:
```
...
export const initialState: State = {
  open: false,
  item: {breadcrumb: [], data: null},
  items: [] // <== elenco delle voci di menu
};
...
```

le informazioni necessarie per la creazione di una nuova voce di menu cliccabile sono:
    label 
        "Coin"  
    icona:
        "i pi-fw pi-user-plus"   
    rotta web
        coin

nuova voce di menu da aggiungere all'attributo `items`
```
  {
    label: 'Coin',
    icon: 'pi pi-fw pi-user-plus', 
    command: (event$) => {
      // invoco il router per cambiare pagina
      event$.item.store$.dispatch(RouterStoreActions.RouterGo({path: ['coin']}));

      // salvo nello store del menù l'elemento selezionato.
      event$.item.store$.dispatch(SlideMenuStoreActions.Select({
        item: {
          data: {},
          breadcrumb: ['Sezione ', 'Coin'] // breadcrumb 
        }
      }));
    }
  }

```
