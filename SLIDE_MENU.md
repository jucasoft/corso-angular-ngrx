# Reactive form
Modificha del menu, per permettere l'apertura delle sezioni create.
Prerequisito: creare l'applicaizone seguendo il tutorial [ngrx-entity-crud](https://www.npmjs.com/package/ngrx-entity-crud)

Il componente del menu che dobbiamo modificare fa parte della libreria di [PrimeNg](https://primefaces.org/primeng/showcase/), in particolare dobbiamo modificare la lista di [MenuModel](https://primefaces.org/primeng/showcase/#/menumodel)

aprire file: "src/app/main/components/slide-menu/slide-menu.component.ts"
l'elenco delle voci di menu sono l'attributo:
```
...
items: MenuItem[];
...
```

vengono settate staticamente nel metodo ngOnInit:
```
...
  ngOnInit(): void {
    this.items = [{
      label: 'File (demonstrative)',
      items: [
        {label: 'New  (demonstrative)', icon: 'pi pi-fw pi-plus'},
        {label: 'Download  (demonstrative)', icon: 'pi pi-fw pi-download'}
      ]
    },
      {
        label: 'Edit (demonstrative)',
        items: [
          {label: 'Add User (demonstrative)', icon: 'pi pi-fw pi-user-plus'},
          {label: 'Remove User (demonstrative)', icon: 'pi pi-fw pi-user-minus'}
        ]
      }];
}
...
```

per prima cosa dobbiamo cancellare tutte le voci di menu presenti:
```
...
  ngOnInit(): void {
    this.items = [];
  }
...
```

creaiamo una voce di menu di tipo MenuModel per aprire una sezione dell'applicazione.
le informazioni che ci necessitano sono:
    la stringa che vogliamo appaia nel menu  
        "Coin"  
    l'icona del menu  
        "i pi-fw pi-user-plus"   
    rotta web
        coin

```
this.items = [
  {
    label: 'User',
    icon: 'pi pi-fw pi-user-plus',
    command: (event$) => {
      // invoco il router per cambiare pagina
      this.store$.dispatch(RouterStoreActions.RouterGo({path: ['coin']}));

      // salvo nello store del menù l'elemento selezionato.
      this.store$.dispatch(SlideMenuStoreActions.Select({
        item: {
          data: {},
          breadcrumb: ['Sezione ', 'Coin'] // breadcrumb 
        }
      }));
    }
  }
];
```
