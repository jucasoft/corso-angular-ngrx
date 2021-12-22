# Reactive form
Prerequisito: creare l'applicaizone seguendo il tutorial [ngrx-entity-crud](https://www.npmjs.com/package/ngrx-entity-crud)

ipotizzando di avere la classe Coin come segue:
```
export class Coin {
  public id: string = undefined;
  public name: string = undefined;
  public value: string = undefined;
  static selectId: (item: Coin) => string = item => item.id;
}
```

aprire file: "src/app/main/views/coin/coin-edit/coin-edit.component.ts"
```
...
export class CoinEditComponent extends PopUpBaseComponent<Coin> {

  form: FormGroup; // form

  id: FormControl; // attributo
  name: FormControl; // attributo
  value: FormControl; // attributo

  setItemPerform(value: Coin): void {
    this.makeFrom();
    this.form.reset(value);
  }

  makeFrom(): void {
    this.id = this.fb.control({value: '', disabled: true});
    this.name = this.fb.control('', Validators.required);
    this.value = this.fb.control('', Validators.required);

    this.form = this.fb.group({ //form
      id: this.id, // attributo
      name: this.name, // attributo
      value: this.value // attributo
    });
  }
...
```

aprire file: "src/app/main/views/coin/coin-edit/coin-edit.component.html"
```
...
  <form
    class="dynamic-form"
    [formGroup]="form">

    <div class="p-grid">
      <div class="p-col">
        <label for="id"><strong>id</strong></label><br>
        <input id="id" name="id" type="text" class="form-control" pInputText [formControl]="id"/>
      </div>
    </div>

    <div class="p-grid">
      <div class="p-col">
        <label for="name"><strong>name</strong></label><br>
        <input id="name" name="name" type="text" class="form-control" pInputText [formControl]="name"/>
      </div>
    </div>

    <div class="p-grid">
      <div class="p-col">
        <label for="value"><strong>value</strong></label><br>
        <input id="value" name="value" type="text" class="form-control" pInputText [formControl]="value"/>
      </div>
    </div>

  </form>
...
```

aggiungere al pulsante "save":
```
[disabled]="!form.valid"
```

## validatori

verificare che siano presenti i seguenti file:
 - src/app/core/components/form-error-msg/form-error-msg.component.ts
 - src/app/core/components/form-error-msg/form-error-msg.module.ts
 - src/app/core/utils/j-validators.ts

se non fossero presti recuperarli da [ngrx-entity-crud-prime-ng-boilerplate](https://github.com/jucasoft/ngrx-entity-crud-prime-ng-boilerplate)

aprire il file: "src/app/main/views/coin/coin-edit/coin-edit.component.ts"
aggiungere validatori dalla classe "JValidators", ad esempio:

```
...
  makeFrom(): void {
    this.id = this.fb.control({value: '', disabled: true});
    this.name = this.fb.control('', JValidators.required());
    this.value = this.fb.control('', [JValidators.required(), JValidators.maxLength(2)]);
...
```

aprire il file: "src/app/main/views/coin/coin-edit/coin-edit.component.html"
modificare

```
...
<div class="p-grid">
  <div class="p-col">
    <label for="name"><strong>name</strong></label><br>
    <input id="name" name="name" type="text" class="form-control" pInputText [formControl]="name"/>
    <app-form-error-msg [fc]="name"></app-form-error-msg>  <!-- componente da aggiungere -->
  </div>
</div>
...
```

## cambiare dinamicamente dei validatori
alla modifica di un campo (FirstField), abilito il validatore su un secondo campo (SecondField) dipendente.
```
makeFrom(): void {

...

this.FirstField.valueChanges.subscribe(val => {
  if(val){
    this.SecondField.setValidators([Validators.required]);
    this.SecondField.updateValueAndValidity();
    this.SecondField.enable();
  } else {
    this.SecondField.clearValidators();
    this.SecondField.updateValueAndValidity();
    this.SecondField.disable();

  }
});
```
