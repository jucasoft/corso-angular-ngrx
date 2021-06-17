# creare un componente reactive form che estenda ng-select
# parte grafica
<ng-select
[items]="items"
[bindValue]="bindValue"
[bindLabel]="bindLabel"
[multiple]="true"
[(ngModel)]="_value"
[disabled]="_disabled"
(change)="_onChange($event)"
(focus)="_onTouched($event)"
</ng-select>

# ricordarsi del CUSTOM_VALUE_ACCESSOR
const CUSTOM_VALUE_ACCESSOR: any = {
  provide: NG_VALUE_ACCESSOR,
  useExisting: forwardRef(() => ...),
  multi: true,
};

# aggiungere il CUSTOM_VALUE_ACCESSOR come provider
providers: [CUSTOM_VALUE_ACCESSOR],

# bozza di classe
class ... implements ControlValueAccessor {
...

_onChange: any;
_onTouched: any;
_disabled: boolean;
_value: any;

  registerOnChange(fn: any): void {
    this._onChange = fn;
  }

  registerOnTouched(fn: any): void {
    this._onTouched = fn;
  }

  setDisabledState(isDisabled: boolean): void {
    this._disabled = isDisabled;
  }

  writeValue(obj: any): void {
    this._value = obj;
  }
