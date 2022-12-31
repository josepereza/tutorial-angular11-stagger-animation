Tutorial from DesignCourse: Angular Stagger Animations Tutorial (4.2+)
https://www.youtube.com/watch?v=h-bUT5BMQrI

Note: moved [@listAnimation]="items.length" from the container div to a new div to get the example to run as expected.

## Tutorial - stagger

Para crear un efecto de fade-in con stagger (aparición gradual en serie) en Angular utilizando la biblioteca de animaciones de Angular, debes seguir los mismos pasos que en las respuestas anteriores, pero con algunas modificaciones en el código de animación.

    Asegúrate de tener instalado el módulo @angular/animations en tu proyecto Angular. Si no lo tienes instalado, ejecuta npm install --save @angular/animations.

    En el archivo app.module.ts, agrega BrowserAnimationsModule a la lista de importaciones y a @NgModule.imports.
    
    ```
    import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

@NgModule({
  imports: [BrowserAnimationsModule],
  ...
})
export class AppModule { }

    ```
    En el componente donde quieres aplicar el efecto de fade-in con stagger, importa el módulo @angular/animations y define el estado y la transición de animación en el archivo de componente. Por ejemplo:
    
...
import { trigger, state, transition, style, animate, query, stagger } from '@angular/animations';

@Component({
  selector: 'app-my-component',
  templateUrl: './my-component.component.html',
  styleUrls: ['./my-component.component.css'],
  animations: [
    trigger('fadeInStagger', [
      transition('* => *', [
        query(':enter', [
          style({opacity: 0, transform: 'translateY(-15px)'}),
          stagger(100, [
            animate('600ms', style({opacity: 1, transform: 'translateY(0)'})),
          ])
        ], {optional: true})
      ])
    ])
  ]
})
export class MyComponentComponent { ... }

...

En este ejemplo, hemos definido una transición que se aplica a cualquier cambio de estado y que consiste en una consulta a todos los elementos que entran en el estado (:enter). Estos elementos tienen una opacidad inicial de 0 y un desplazamiento vertical inicial de -15px. Luego, se aplica un stagger de 100ms entre cada elemento y se anima la opacidad y el desplazamiento vertical durante 600ms para que vuelvan a su estado inicial.

    En la etiqueta HTML donde quieres aplicar el efecto de fade-in con stagger, agrega la directiva [@fadeInStagger] a cada elemento que quieras que tenga el efecto. Por ejemplo:
    
...
<div [@fadeInStagger]>
  <div>Elemento 1</div>
  <div>Elemento 2</div>

...
