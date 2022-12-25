# AngularTourOfHeroes

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 14.2.3.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.

step to step

1. creamos el proyecto
ng new angular-tour-of-heroes

2. ejecutamos el proyecto
ng serve --open

3. cambiamos el titulo de la aplicacion
app.component.ts

title = 'Tour of Heroes';

4. el titulo se visualiza en la interface html en este tag:
<span>{{ title }} app is running!</span>

5. en el archivo que existe src/styles.css y esta vacio, ingresamos estos valores;

/* Application-wide Styles */
h1 {
  color: #369;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 250%;
}
h2, h3 {
  color: #444;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: lighter;
}
body {
  margin: 2em;
}
body, input[type="text"], button {
  color: #333;
  font-family: Cambria, Georgia, serif;
}
button {
  background-color: #eee;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  color: black;
  font-size: 1.2rem;
  padding: 1rem;
  margin-right: 1rem;
  margin-bottom: 1rem;
  margin-top: 1rem;
}
button:hover {
  background-color: black;
  color: white;
}
button:disabled {
  background-color: #eee;
  color: #aaa;
  cursor: auto;
}

/* everywhere else */
* {
  font-family: Arial, Helvetica, sans-serif;
}

6. creamos un componente
ng generate component heroes

7. generado el componente en la interfas html tiene un mensaje estatico, vamos a modificar
el fichero ts para incluir una variable y que el valor se visualice en el html

heroes.component.ts
hero = 'Windstorm';

heroes.component.html
<h2>{{hero}}</h2>

8. generado el componente incluimos un tag en app.componente.html para visualizar el contenido:
    <app-heroes></app-heroes>

9. creamos el modelo llamado interface por Angular, lo creamos en el componente directorio
hero.ts

export interface Hero {
  id: number;
  name: string;
}

10. vamos modificando el proyecto inicializado el servicio asi detectamos errores
ng serve

11. modificamos heroes.componente.ts para incluir la interface

export class HeroesComponent implements OnInit {
  hero: Hero = {
    id: 1,
    name: 'Windstorm'
  };

12. relacionamos el modelo con la vista Two-way binding
<div>
  <label for="name">Hero name: </label>
  <input id="name" [(ngModel)]="hero.name" placeholder="name">
</div>

produce un error no reconoce ngModel porque necesita FormsModule

modificamos app.module.ts agregando:
import { FormsModule } from '@angular/forms'; // <-- NgModel lives here

imports: [
  FormsModule
],

Nota. por defecto al crear los componente estos ya se incluyeron en el modulo de esta forma, solo es comprobar:
@NgModule({
  declarations: [
    AppComponent,
    HeroesComponent
  ],

13. creamos una lista para visualizar en la vista, creamos un mock; mock-heroes.ts
import { Hero } from './hero';

export const HEROES: Hero[] = [
  { id: 12, name: 'Dr. Nice' },
  { id: 13, name: 'Bombasto' },
  { id: 14, name: 'Celeritas' },
  { id: 15, name: 'Magneta' },
  { id: 16, name: 'RubberMan' },
  { id: 17, name: 'Dynama' },
  { id: 18, name: 'Dr. IQ' },
  { id: 19, name: 'Magma' },
  { id: 20, name: 'Tornado' }
];

14. para visualizar en la vista agregamos en heroes.component.ts lo siguiente

import { HEROES } from '../mock-heroes';

heroes = HEROES;

15. hacemos un iterate en la vista para pintar la lista de objetos HEROES
