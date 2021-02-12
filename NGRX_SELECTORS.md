#NGRX_ENTITY_CRUD_DOC

##di seguito elencate tutte le action con relative spiegazioni:

- ###SearchRequest
    - azione utilizzata per eseguire delle ricerche asincrone
    - **parametri necessari**:
        - mode?: 'REFRESH' | 'upsertMany' | 'addAll';
        - queryParams?: any; 
        - path?: any[];
        - onFault?: Action[];
        - onResult?: Action[];
        - dispatchResponse?: boolean;
        - type: string
 ring;