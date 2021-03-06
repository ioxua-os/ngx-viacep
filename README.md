

# Ngx-Viacep!

Uma biblioteca Angular para busca de CEP e endereços pelo serviço [ViaCep](https://viacep.com.br/). Utiliza o Módulo HttpClientModule, portanto, é recomendado seu uso a partir da verão 4.3 do Angular.

|Serviço|Master|Staging|Develop|
|--|--|--|--|
|CircleCI|[![CircleCI](https://circleci.com/gh/brunoc107/ngx-viacep/tree/master.svg?style=svg)](https://circleci.com/gh/brunoc107/ngx-viacep/tree/master)|[![CircleCI](https://circleci.com/gh/brunoc107/ngx-viacep/tree/staging.svg?style=svg)](https://circleci.com/gh/brunoc107/ngx-viacep/tree/staging)|[![CircleCI](https://circleci.com/gh/brunoc107/ngx-viacep/tree/develop.svg?style=svg)](https://circleci.com/gh/brunoc107/ngx-viacep/tree/develop)|

## Instalação  
  
Via npm:  
  
```bash  
$ npm install @brunoc/ngx-viacep --save
```  
  
Via yarn:  
  
```bash  
$ yarn add @brunoc/ngx-viacep
```  
  
## Instruções  
  
No módulo onde for necessário buscar CEP, importar ``NgxViacepModule`` e adicionar aos imports, como no exemplo abaixo:

```typescript  
import { BrowserModule } from '@angular/platform-browser';  
import { NgModule } from '@angular/core';  
  
import { NgxViacepModule } from '@brunoc/ngx-viacep';  
  
import { AppComponent } from './app.component';  
  
@NgModule({  
  declarations: [  
    AppComponent 
  ],
  imports: [  
    BrowserModule, 
    NgxViacepModule
  ],  
  bootstrap: [AppComponent]  
})  
export class AppModule { }  
```  
  
No componente onde a funcionalidade for necessária, importar o serviço ``NgxViacepService`` e injetá-lo:  
  
```typescript  
import { Component } from '@angular/core';  
import { OnInit } from '@angular/core/';  
  
import { NgxViacepService } from '@brunoc/ngx-viacep';  
  
@Component({  
  selector: 'app-root',  
  templateUrl: './app.component.html',  
  styleUrls: ['./app.component.css']  
})  
export class AppComponent implements OnInit {  
  
  title = 'app';  
  constructor( private viacep: NgxViacepService ) {}  
  
  ngOnInit() {}  
}  
```
  
## Buscar endereço por cep  
O serviço "NgxViacepService" possui um método para a busca de endereço por CEP, que retorna uma Promise, seu uso pode ser visto abaixo:  
```typescript  
this.viacep.buscarPorCep('01001000').then( ( endereco: Endereco ) => {  
 // Endereço retornado :) console.log(endereco);  
}).catch( (error: ErroCep) => {  
 // Alguma coisa deu errado :/ console.log(error.message);  
});  
```  
As interfaces "Endereco" e "ErroCep" podem ser importadas da mesma maneira que o serviço, como no exemplo:  
```typescript  
import { NgxViacepService, Endereco, ErroCep } from '@brunoc/ngx-viacep';  
```  

## Busca sem CEP  
Para buscar um endereço cujo cep não é conhecido, pode-se utilizar o método a seguir:  
```typescript  
this.viacep.buscarPorEndereco('rs', 'porto alegre', 'domingos').then( (enderecos: Endereco[]) => {  
 // Array de endereços possíveis retornados :D console.log(enderecos);  
}).catch( (error: ErroCep) => {  
 // Ocorreu algum erro :/ console.log(error.message);  
});  
```  

O método "buscarPorEndereco" faz uma pesquisa e retorna uma lista de endereços no estado e cidade definidos, cujo logradouro possua no nome o valor passado no terceiro argumento.  

## License  
MIT © [Bruno Carvalho](mailto:brunocarvalho107@gmail.com)
