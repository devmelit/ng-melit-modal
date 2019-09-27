# NgMelitModal

Modal de confirmación de [Bootstrap](https://ng-bootstrap.github.io/#/getting-started) para Angular 5+  
<https://ng-bootstrap.github.io/#/getting-started>


## Instalación

_Es necesario que el proyecto tenga Bootstrap 4_

`npm i ng-melit-modal`

## Cómo usar

Primero deberemos importarlo en el module

_app.module.ts Sin lazy loading_
o _xxxx.module.ts Con Lazy Loading_

```typescript
@NgModule({
    declarations: [...],
    imports: [...,NgMelitModalModule],
    entryComponents: [...,NgMelitModalComponent],
    ...
})
```

En el componente donde queramos usarlo 

_xxxx.component.ts Con opciones predeterminadas_

```typescript
import { Component } from '@angular/core';
import { NgMelitModalService , ConfirmOptions } from 'ng-melit-modal';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  
  respuesta : string;

  constructor(private modalConfirm: NgMelitModalService) { }

///Metodo con el cual abrimos la modal
  openModal() {

      //Si no queremos añadir opciones especiales no pasamos parametro

    this.modalConfirm.confirm().then(resp => {
        
        //Aqui obtendremos a que botón ha dado el usuario
       this.respuesta = resp;
    
    });
  }
}
```

### Como personalizar los mensajes de la modal
___

La configuración de los mensajes de la modal, se hace instanciando un objeto de la Clase _ConfirmOptions_

| Atributos     | Definición    | Valor por Defecto | Tipo | 
| ------------- |:-------------:| :-----:| :----: |
| _title_      | Titulo superior de la modal | Confirmacion | `string` |
| _message_      | Mensaje de la modal      | ¿Desea confirmar su acción? | `string` | 
| _msgBtnOk_ | Texto que mostrará el botón que confirme | Aceptar | `string` |
| _msgBtnCancel_ | Texto que mostrará el botón que cancele | Cancelar | `string` |
| _valueAccept_ | Valor que nos devolverá la modal cuando den al botón de aceptar| ok | `string` |
| _valueCancel_ | Valor que nos devolverá la modal cuando den al botón de cancelar| cancel | `string` |
| _showCancel_ | Muestra el boton de cancelar | true | `boolean` |
| _modalClass_ | Clase de **Bootstrap** con la que se presentara la modal | - | `string` |
| _textClass_ | Clase de **Bootstrap** con la que se presentara el texto de la modal | dark | `string` |
| _btnOkClass_ | Clase de **Bootstrap** con la que se presentara el botón de confirmación | btn-outline-primary | `string` |
| _btnCancelClass_ | Clase de **Bootstrap** con la que se presentara el botón de cancelación | btn-outline-danger | `string` |
| _btnOkTextClass_ | Clase de **Bootstrap** con la que se presentara el color del texto botón de confirmación | - | `string` |
| _btnCancelTextClass_ | Clase de **Bootstrap** con la que se presentara el color del texto botón de cancelación | - | `string` |


Por lo que si queremos hacer que tengan distitos valores, lo haremos de la siguiente manera: 

```typescript
    openModal() {

    //En caso de que cambiemos todos los campos
    let customOpts: ConfirmOptions = {
      title: 'Confirmacion Personalizada',
      message: 'Mensaje Personalizado',
      msgBtnOk: 'Boton Ok personalizado',
      msgBtnCancel: 'Boton Cancelar Personalizado',
      valueAccept: 'Valor Ok personalizado',
      valueCancel: 'Valor Cancel Personalizado',
      modalClass: 'warning',
      textClass: 'primary',
      showCancel: false,
      btnCancelClass: '',
      btnOkClass: 'btn-primary',
      btnCancelTextClass: 'text-primary',
      btnOkTextClass: 'text-primary',
    }

    //En caso de que solo queramos cambiar algunos

    let customOpts2 : ConfirmOptions = new ConfirmOptions();
    customOpts.title = 'Confirmacion Personalizada';

    //Y lo pasamos como parametro 
    this.modalConfirm.confirm(customOpts).then(resp => {
        
        //Aqui obtendremos a que botón ha dado el usuario
       this.respuesta = resp;
    
    });
  }
```


