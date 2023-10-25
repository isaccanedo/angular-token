![Angular-Token](https://raw.githubusercontent.com/neroniaky/angular-token/master/docs/angular-token-logo.png)

[![npm version](https://badge.fury.io/js/angular-token.svg)](https://badge.fury.io/js/angular-token)
[![npm downloads](https://img.shields.io/npm/dt/angular-token.svg)](https://npmjs.org/angular-token)
[![Build Status](https://travis-ci.org/neroniaky/angular-token.svg?branch=master)](https://travis-ci.org/neroniaky/angular-token)
[![Angular Style Guide](https://mgechev.github.io/angular2-style-guide/images/badge.svg)](https://angular.io/styleguide)

🔑 Serviço de autenticação baseado em token para Angular com interceptor e suporte multiusuário. Funciona melhor com o [devise token auth](https://github.com/lynndylanhurley/devise_token_auth) gem para Rails.

👋 Esta biblioteca foi renomeada para **Angular-Token**! Siga o [guia de migração](https://angular-token.gitbook.io/docs/migrate-to-7).

---

### Links Rápidos

- 🚀 View to demo on [Stackblitz](https://stackblitz.com/github/neroniaky/angular-token)
- ✨ Learn about it on the [docs site](https://angular-token.gitbook.io/docs)
- 🔧 Support us by [contributing](https://angular-token.gitbook.io/docs/contribute)

---

## Instalar
0. Configure um Rails com [Devise Token Auth](https://github.com/lynndylanhurley/devise_token_auth)

1. Instale Angular-Token via NPM com
    ```bash
    npm install angular-token
    ```

2. Importe e adicione `AngularTokenModule` ao seu módulo principal e chame a função 'forRoot' com o arquivo config. Certifique-se de ter importado `HttpClientModule` também.
    ```javascript
    import { AngularTokenModule } from 'angular-token';

    @NgModule({
        imports: [
            ...,
            HttpClientModule,
            AngularTokenModule.forRoot({
              ...
            })
        ],
        declarations: [ ... ],
        bootstrap:    [ ... ]
    })
    ```

3. (Talvez opcional) Corrigir erro de tempo de execução do contexto de injeção
After installing this package, if you get an `Error: inject() must be called from an injection context` when running your app, add the following to your typescript path config in the `tsconfig[.app].json` file:
    ```json
    "paths": {
      "@angular/*": [ "./node_modules/@angular/*" ]
    }
    ```

## Use

1. Register your user
    ```javascript
    constructor(private tokenService: AngularTokenService) { }

    this.tokenService.registerAccount({
        login:                'example@example.org',
        password:             'secretPassword',
        passwordConfirmation: 'secretPassword'
    }).subscribe(
        res =>      console.log(res),
        error =>    console.log(error)
    );
    ```

2. Sign in your user
    ```javascript
    constructor(private tokenService: AngularTokenService) { }

    this.tokenService.signIn({
        login:    'example@example.org',
        password: 'secretPassword'
    }).subscribe(
        res =>      console.log(res),
        error =>    console.log(error)
    );
    ```

3. Now you can use HttpClient to access private resources
    ```javascript
    constructor(http: HttpClient) { }

    this.http.get('private_resource').subscribe(
        res =>      console.log(res),
        error =>    console.log(error)
    );
    ```
