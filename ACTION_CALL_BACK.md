come creare un'azione di callBack  
caso d'uso:
  ho una lista con 10 elementi
  ne seleziono uno
  dispaccio l'azione per il caricamento completo dell'elemento
  al caricamento completato devo aprire una popUp con il dato caricato dal BE
  

l'oggetto deve avere due attributi: "type" e "newAction":  
  - type: string  
  - newAction: (response, action) => Action   
 
descrizione:

- type => di tipo stringa non verrà mai utilizzato, serve solo a far interpretare questo aggetto come se fosse una Action  
- newAction => in questo attributo, si può passare una funzione che accetta in ingresso la response della chiamata remota e la action da cui ha avuto origine  

esempio:
```ts
const afterAction = {
  type: 'afterEditCreateAction',
  newAction: (response, action) => { // <== response: risposta dal BE, action: action passata inizialmente.
    // ... ritorno l'azione che verrà dispacciata nell'effect.
  }
};
```

in questo esempio dove viene passata alla collBack Action anche un id, necessario in fase di creazione della callBackAction
```ts
const afterAction = {
  type: 'afterEditCreateAction',
  newAction: ((id) => (response, action) => {
    return LoReIpsumStoreActions.Edit({item: {id, data: response.data}});
  })(id)
};
```

come usare questa azione:
```ts
this.store$.dispatch(LoReIpsumStoreActions.Edit({item: {...oggettoDaModificare}, onResult:['afterAction']}))
```
