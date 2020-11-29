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
