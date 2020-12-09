# Custom columns
Prerequisito: creare l'applicaizone seguendo il tutorial [ngrx-entity-crud](https://www.npmjs.com/package/ngrx-entity-crud)

aprire file: "src/app/main/views/coin/coin-list/coin-list.component.ts"
```
export class CoinListComponent implements OnInit {

  collection$: Observable<Coin[]>;

  constructor(private store$: Store<RootStoreState.State>,
              private confirmationService: ConfirmationService) {
    console.log('CoinListComponent.constructor()');
  }

  ngOnInit() {
    console.log('CoinListComponent.ngOnInit()');
    this.collection$ = this.store$.select(CoinStoreSelectors.selectAll);
    this.store$.dispatch(
      CoinStoreActions.SearchRequest({queryParams: {}})
    );
  }
```

aprire file: "src/app/main/views/coin/coin-list/coin-list.component.html"
```
<p-table [value]="collection$ | async">
  <ng-template pTemplate="header">
    <tr>
      <th>
        id
      </th>
      <th>
        name
      </th>
      <th>
        value
      </th>
      <th>actions</th>
    </tr>
  </ng-template>
  <ng-template pTemplate="body" let-item>
    <tr>
      <td>
        {{item['id']}}
      </td>
      <td>
        {{item['name']}}
      </td>
      <td>
        {{item['value']}}
      </td>
      <td>
        <p-button icon="fa fa-edit" class="mr-1" (click)="onEdit(item)"></p-button>
        <p-button icon="fa fa-copy" class="mr-1" (click)="onCopy(item)"></p-button>
        <p-button icon="fa fa-trash" class="mr-1 p-button-danger"  (click)="onDelete(item)"></p-button>
      </td>
    </tr>
  </ng-template>
</p-table>
```
