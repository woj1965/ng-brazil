# Ng-Brazil

Angular5 pipes / directives / validators / mask for brazillian like apps

This project was tested integrated with the following techs:

* angular5
* angular-material
* ionic3 (masks is not fully working, that is an issue for that, but pipes/directives/validators/mask)

Modules:

* CPF 
* CNPJ
* RG
* Inscrição Estadual
* Telefone
* CEP

See the demo working project:


![Demo Image](/src/assets/print.png)


## Installation

To install this library with npm, run below command:

$ npm install --save ng-brazil  angular2-text-mask 


 
## Usage

### Configuration

Import module in root

```ts
import { NgBrazil } from 'ng-brazil' 

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    ....,
    NgBrazil
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

If you would like to use masks import module;

```ts
import { TextMaskModule } from 'angular2-text-mask';

imports: [
    ....,
    TextMaskModule,
    NgBrazil
  ], 
```


Then setup your component models as below :

```ts
import { Component, ViewChild } from '@angular/core';
import { MASKS } from 'ng-brazil';

@Component({
  selector: 'app-root',
  template: '<input type="text" [cpf]>',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  public MASKS = MASKS;
  
  constructor() { 
    this.formFields = {
      estado: [''],
      cpf: ['', [<any>Validators.required, <any>NgBrazilValidators.cpf]],
      cnpj: ['', [<any>Validators.required, <any>NgBrazilValidators.cnpj]],
      rg: ['', [<any>Validators.required, <any>NgBrazilValidators.rg]],
      cep: ['', [<any>Validators.required, <any>NgBrazilValidators.cep]],
      telefone: ['', [<any>Validators.required, <any>NgBrazilValidators.telefone]],
      inscricaoestadual: ['', [<any>Validators.required, <any>NgBrazilValidators.inscricaoestadual(this.estado)]]
    };
    this.form = this.fb.group(this.formFields);
  }

}
```

## Forms and Mask

```html
<input type="text" formControlName="cnpj" cnpj [textMask]="{mask: MASKS.cnpj.textMask}">
<input type="text" formControlName="cpf" cpf [textMask]="{mask: MASKS.cpf.textMask}">
<input type="text" formControlName="rg" rg [textMask]="{mask: MASKS.rg.textMask}"> 
<input type="text" formControlName="inscricaoestadual" inscricaoestadual="mg" [textMask]="{mask: MASKS.inscricaoestadual[estado].textMask}">
<input type="text" formControlName="telefone" telefone #telefone [textMask]="{mask: MASKS.telefone.textMaskFunction(telefone.value)}">
<input type="text" formControlName="cep" cep [textMask]="{mask: MASKS.cep.textMask}">
```
## Pipes

```html
CPF: From 12345678910 to {{'12345678910' | cpf}} <br/>
CNPJ: From 40841253000102 to {{'40841253000102' | cnpj}} <br/>
RG: From MG10111222 to {{'MG10111222' | rg}} <br/>
Inscrição Estadual: From 0018192630048 to {{'0018192630048' | inscricaoestadual: 'mg'}} <br/>
Telefone: From 3199998888 to {{'3199998888' | telefone}} <br/>
```

# Demo
Demo component files are included in Git Project.

Demo Project:
[https://github.com/mariohmol/ng-brazil/tree/master/src/app/demo)

Used as reference the pipes/validators from:

* https://github.com/yuyang041060120/ng2-validation
* https://github.com/text-mask/text-mask


# TODO

There is some issues to work with, check it out

# License
MIT(./LICENSE)