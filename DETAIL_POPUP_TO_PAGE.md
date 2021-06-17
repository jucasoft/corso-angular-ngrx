Procedura per trasformare una pagina di popUp in Datail. 
sostituzione classi:
    sostituire la classe PopUpData con DetailData (classi che fanno da vettore)
    modificare le rotte da "{outlets: {popUp: ['????']}}" a '????'
    modificare l'estensione da PopUpBaseComponent a DetailBaseComponent


Modifiche da apportare al codice:
- {nomeClasse}EditComponent.ts
    sostituire l'estensione da PopUpBaseComponent a DetailBaseComponent

- {nomeClasse}ListComponent.ts
    sostituire la classe (che fa da vettore) da: PopUpData a DetailData
    sostituire l'azione da RouterGoPopUp a RouterGo
    modificare le rotte da "{outlets: {popUp: ['????']}}" a '????'
    
- ButtonNew{nomeClasse}Component.ts
    PopUpData to DetailData
    RouterGoPopUp to RouterGo
    modificare la rotta da "{outlets: {popUp: ['edit']}}" a 'edit'
