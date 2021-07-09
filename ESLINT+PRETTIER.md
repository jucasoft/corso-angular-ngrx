# ESLINT + PRETTIER

integrazione eslint + prettier

## prerequisiti

- prima di cominciare con la procedura, committare tutto, in modo da poter revertare in caso di errori.

## procedura

-	seguire il tutorial a questo link

	https://github.com/angular-eslint/angular-eslint

consiste in varie sezioni, come installazione eslint partendo da un progetto senza alcun lint
o la migrazione da tslint a eslint, inoltre mostra la giusta procedura per integrare prettier senza conflitti con eslint

-	se effettui la migrazione da tslint a eslint potresti trovare nel file eslint librerie non adatte al tuo progetto, è consigliato sostituire il file
     .eslintrc.json con uno base, esempio:

```
{
  "root": true,
  "ignorePatterns": [
    "projects/**/*"
  ],
  "overrides": [
    {
      "files": [
        "*.ts"
      ],
      "parserOptions": {
        "project": [
          "tsconfig.json
        ],
        "createDefaultProgram": true
      },
      "extends": [
        "plugin:@angular-eslint/recommended",
        "plugin:@angular-eslint/template/process-inline-templates",
        "plugin:prettier/recommended"
      ],
      "rules": {
        "@angular-eslint/directive-selector": [
          "error",
          {
            "type": "attribute",
            "prefix": "app",
            "style": "camelCase"
          }
        ],
        "@angular-eslint/component-selector": [
          "error",
          {
            "type": "element",
            "prefix": "app",
            "style": "kebab-case"
          }
        ],
        "@angular-eslint/no-empty-lifecycle-method": "off",
        "@angular-eslint/no-output-on-prefix": "off",
        "space-before-function-paren": "off",
        "@angular-eslint/contextual-lifecycle": "off",
        "@angular-eslint/use-lifecycle-interface": "off",
        "eqeqeq": "off",
        "no-console": "off",
        "space-in-parens": [
          "off",
          "never"
        ]
      }
    },
    {
      "files": [
        "*.html"
      ],
      "extends": [
        "plugin:@angular-eslint/template/recommended"
      ],
      "rules": {}
    },
    {
      "files": [
        "*.html"
      ],
      "excludedFiles": [
        "*inline-template-*.component.html"
      ],
      "extends": [
        "plugin:prettier/recommended"
      ],
      "rules": {
        // NOTE: WE ARE OVERRIDING THE DEFAULT CONFIG TO ALWAYS SET THE PARSER TO ANGULAR (SEE BELOW)
        "max-len": [
          "error",
          {
            "code": 250,
            "ignoreUrls": true
          }
        ],
        "prettier/prettier": [
          "error",
          {
            "parser": "angular",
          }
        ]
      }
    }
  ]
}
```

## possibili errori

- error  Parsing error: Unexpected token <

soluzione: specificare il parser angular per i file html come segue

```
rules{
	"prettier/prettier": [
	  "error",
	  {
		"parser": "angular"
	  }
	]
}
```
