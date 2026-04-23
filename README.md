![Angular-Token](https://raw.githubusercontent.com/neroniaky/angular-token/master/docs/angular-token-logo.png)

[![npm version](https://badge.fury.io/js/angular-token.svg)](https://badge.fury.io/js/angular-token)
[![npm downloads](https://img.shields.io/npm/dt/angular-token.svg)](https://npmjs.org/angular-token)
[![Build Status](https://travis-ci.org/neroniaky/angular-token.svg?branch=master)](https://travis-ci.org/neroniaky/angular-token)
[![Angular Style Guide](https://mgechev.github.io/angular2-style-guide/images/badge.svg)](https://angular.io/styleguide)

🔑 Serviço de autenticação baseado em token para Angular com interceptor e suporte multiusuário. Funciona melhor com o [conceber autenticação de token](https://github.com/lynndylanhurley/devise_token_auth) gem para Rails.

👋 Esta biblioteca foi renomeada para **Angular-Token**! Siga o [guia de migração](https://angular-token.gitbook.io/docs/migrate-to-7).

---

## Links Rápidos

- 🚀 Ver para demonstração em [Stackblitz](https://stackblitz.com/github/neroniaky/angular-token)
- ✨ Aprenda sobre isso no [docs site](https://angular-token.gitbook.io/docs)
- 🔧 Apoie-nos por [contributing](https://angular-token.gitbook.io/docs/contribute)

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
Depois de instalar este pacote, se você receber um `Erro: inject() deve ser chamado a partir de um contexto de injeção` ao executar seu aplicativo, adicione o seguinte à configuração do caminho do TypeScript no arquivo `tsconfig[.app].json`:
    ```json
    "paths": {
      "@angular/*": [ "./node_modules/@angular/*" ]
    }
    ```

## Usar

1. Cadastre seu usuário
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

2. Faça login com seu usuário
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

3. Agora você pode usar HttpClient para acessar recursos privados
    ```javascript
    constructor(http: HttpClient) { }

    this.http.get('private_resource').subscribe(
        res =>      console.log(res),
        error =>    console.log(error)
    );
    ```
