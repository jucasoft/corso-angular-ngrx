# [TUTORIAL ngrx/store counter](https://ngrx.io/guide/store#tutorial) 
Per prima cosa eseguire il [TUTORIAL counter](https://ngrx.io/guide/store#tutorial) di NGRX,  
!!attenzione, nel punto 1 del tutorial, dopo aver cliccato su "live example" si apre stackblitz.com, in questa pagina prima di iniziare lo sviluppo dovete cliccare sul pulsante blu "Fork".

Dopo aver finito il tutorial online, proviamo ad implementare la medesima funzionalita` sul nostro pc locale.   
Prerequisito: creare l'applicaizone seguendo il tutorial [ngrx-entity-crud](https://www.npmjs.com/package/ngrx-entity-crud)

## New section
crea una nuova sezione grafica con i parametri:
 - clazz "Counter" : corrisponde allo state dello store.
 - lib 'no-libs' : la sezione sara` priva di librerie grafica.
```
ng generate ngrx-entity-crud:section --clazz=Counter --lib=no-libs
```
verranno creati i seguenti file:
```
CREATE src/app/main/views/counter/counter-routing.module.ts (731 bytes)
CREATE src/app/main/views/counter/counter.module.ts (1142 bytes)
CREATE src/app/main/views/counter/counter-edit/counter-edit.component.html (28 bytes)
CREATE src/app/main/views/counter/counter-edit/counter-edit.component.ts (398 bytes)
CREATE src/app/main/views/counter/counter-list/counter-list.component.html (28 bytes)
CREATE src/app/main/views/counter/counter-list/counter-list.component.ts (738 bytes)
CREATE src/app/main/views/counter/counter-main/counter-main.component.html (28 bytes)
CREATE src/app/main/views/counter/counter-main/counter-main.component.ts (400 bytes)
UPDATE src/app/app-routing.module.ts (565 bytes)
```

## New store
crea uno store con i parametri:
 - name "counter" : chiave univoca che identifica la sezione dello store
 - clazz "Counter" : corrisponde allo state dello store.
 - type "BASE" : la versione BASE e priva di tutte le parti per la gesione crud
```
ng generate ngrx-entity-crud:store --name=counter --clazz=Counter --type=BASE
```
verranno creati i seguenti file:
```
CREATE src/app/root-store/counter-store/counter-store.module.ts (816 bytes)
CREATE src/app/root-store/counter-store/actions.ts (325 bytes)
CREATE src/app/root-store/counter-store/effects.ts (311 bytes)
CREATE src/app/root-store/counter-store/index.d.ts (293 bytes)
CREATE src/app/root-store/counter-store/index.ts (291 bytes)
CREATE src/app/root-store/counter-store/names.ts (49 bytes)
CREATE src/app/root-store/counter-store/reducer.ts (327 bytes)
CREATE src/app/root-store/counter-store/selectors.ts (606 bytes)
CREATE src/app/root-store/counter-store/state.ts (125 bytes)
CREATE src/app/main/models/vo/counter.ts (140 bytes)
UPDATE src/app/root-store/index.ts (312 bytes)
UPDATE src/app/root-store/index.d.ts (312 bytes)
UPDATE src/app/root-store/state.ts (196 bytes)
UPDATE src/app/root-store/root-store.module.ts (1060 bytes)
```
## State
aprire il file "src/app/main/models/vo/counter.ts"   
cancellare gli attributi presenti e aggiungere l'attributo "quantity" di tipo "number"   
aprire il file "src/app/root-store/counter-store/state.ts"   
dobbiamo valorizzare lo stato iniziale dello store:
```
export const initialState: Counter = {
  quantity: 0
}
```

## Actions
file: "src/app/root-store/counter-store/actions.ts"  
Dobbiamo creare 3 nuove azioni:
- Increment
- Decrement
- Reset
    
Nel file sono gia` presenti delle azioni d'esempio (ChangeA, ChangeB):
```
export enum ActionTypes {
  CHANGE_A = '[Counter] Change A',
  CHANGE_B = '[Counter] Change b',
}

export const ChangeA = createAction(ActionTypes.CHANGE_A, props<{ valueA: string }>());
export const ChangeB = createAction(ActionTypes.CHANGE_B, props<{ valueB: string }>());
```
creare le nuove azioni modificando le azioni presenti:
```
export enum ActionTypes {
  INCREMENT = '[Counter] increment',
  CHANGE_B = '[Counter] Change b',
}
//NOTA nel nostro caso non abbaimo bisogno di passare valori nell'azione, dobbiamo togliere "props<{ valueA: string }>()"
export const Increment = createAction(ActionTypes.INCREMENT);
export const ChangeB = createAction(ActionTypes.CHANGE_B, props<{ valueB: string }>());
```
la prima azione e` fatta ora dovete creare:
    - Decrement
    - Reset
    
## Reducer
file "src/app/root-store/counter-store/reducer.ts"
modifichiamo lo store come segue:

```
export const featureReducer = createReducer(initialState,
  on(actions.Increment, (state) => {
      console.log('actions.Increment');
      const quantity = state.quantity + 1;
      console.log('quantity', quantity);
      return {quantity};
    },
  ),
  ... aggiungere gli altri metodi ons ...
);
```

## Select
file "src/app/root-store/counter-store/selectors.ts"   
scrivere il seguente codice:
```
import {createFeatureSelector, createSelector, MemoizedSelector} from '@ngrx/store';
import {Names} from './names';
import {Counter} from '@models/vo/counter';

const getQuantity = (state: Counter): number => state.quantity;

export const selectState: MemoizedSelector<object, Counter> = createFeatureSelector<Counter>(Names.NAME);

export const selecQuantity: MemoizedSelector<object, number> = createSelector(
  selectState,
  getQuantity
);

```
## Componente grafico
file "src/app/main/views/counter/counter-main/counter-main.component.ts"   
nel componente e` gia` presente una parte del codice che ci serve, dobbiamo aggiungere 3 metodi:

```
  constructor(private readonly store$: Store<RootStoreState.State>) {
  }

  count$: Observable<number>;

  ngOnInit(): void {
    console.log('CounterMainComponent.ngOnInit()');
    this.count$ = this.store$.select(CounterStoreSelectors.selecQuantity);
  }

  increment(): void {
    console.log('CounterMainComponent.increment()');
    this.store$.dispatch(CounterStoreActions.Increment());
  }

  decrement(): void {
    console.log('CounterMainComponent.decrement()');
    this.store$.dispatch(CounterStoreActions.Decrement());
  }

  reset(): void {
    console.log('CounterMainComponent.reset()');
    this.store$.dispatch(CounterStoreActions.Reset());
  }
```

file: src/app/main/views/counter/counter-main/counter-main.component.html
```
<button (click)="increment()">Increment</button>
<div>Current Count: {{ count$ | async }}</div>
<button (click)="decrement()">Decrement</button>
<button (click)="reset()">Reset Counter</button>
```
