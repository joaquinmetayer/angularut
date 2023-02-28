## Angular Unit Testing Guide

<img width="100%" alt="Screenshot 2023-02-27 at 21 21 56" src="https://user-images.githubusercontent.com/83543601/221725673-629a6649-5ca7-4ee3-8980-e29d086fc824.png">

Creado por **ChatGPT**.
Revisado, corregido dando agregados y aplicado por **Joaquin Metayer**.

Para esos desarrolladores frontend en Angular que quieren aprender a cómo aplicar Unit Testing o Test Unitarios a su código. 

Podría dar más explicaciones y contexto de donde estamos, pero si llegaste a este post solo quieres aprender a como agregar y crear tus propios tests así que vamos con la guía, espero que te sea de ayuda como lo fue para mi crearla. 

**¿Tienes algo para aportar? Pull request y lo vemos!**
Comencemos…

## 1. Configuración inicial

Para empezar, es necesario tener un proyecto de Angular ya creado. Asegúrate de que tienes la última versión de Node.js y Angular CLI instalada. Si no, puedes instalarla utilizando los siguientes comandos:

```
# Instalar Node.js (si no está instalado)

https://nodejs.org/en/

# Instalar Angular CLI

npm install -g @angular/cli
```

## 2. Creación de un componente

Para realizar las pruebas, es necesario tener un componente de Angular. Puedes crear uno con el siguiente comando:

```
ng generate component mi-componente
```

## 3. Estructura del archivo de prueba

Para cada componente, se debe crear un archivo de prueba. Por convención, se suele nombrar el archivo de prueba con la extensión ``.spec.ts`` y ubicarlo en la misma carpeta que el componente que se va a probar.

La estructura básica del archivo de prueba es la siguiente:

```js
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { MiComponenteComponent } from './mi-componente.component';

describe('MiComponenteComponent', () => {
  let component: MiComponenteComponent;
  let fixture: ComponentFixture<MiComponenteComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ MiComponenteComponent ]
    })
    .compileComponents();
  });

  beforeEach(() => {
    fixture = TestBed.createComponent(MiComponenteComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });
});
```

## 4. Descripción del archivo de prueba

### 4.1. Importación de dependencias

```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { MiComponenteComponent } from './mi-componente.component';
```

En esta sección se importan las dependencias necesarias para realizar las pruebas. ``ComponentFixture`` y ``TestBed`` son proporcionados por el módulo ``@angular/core/testing``.

### 4.2. Descripción del componente

```typescript
describe('MiComponenteComponent', () => {
```

En esta sección se describe el componente que se va a probar. El nombre del componente se coloca como primer parámetro de la función ``describe``. El segundo parámetro es una función que contiene todas las pruebas relacionadas con el componente.

### 4.3. Declaración de variables

```typescript
let component: MiComponenteComponent;
let fixture: ComponentFixture<MiComponenteComponent>;
```

En esta sección se declaran las variables necesarias para realizar las pruebas. ``component`` representa una instancia del componente que se va a probar y ``fixture`` representa el componente embebido en un objeto de prueba.

### 4.4. Configuración de TestBed

```typescript
beforeEach(async () => {
  await TestBed.configureTestingModule({
    declarations: [ MiComponenteComponent ]
  })
  .compileComponents();
});
```

En esta sección se configura TestBed. En este caso, se indica que se van a probar componentes y se añade el componente que se va a probar.

### 4.5. Creación de instancia del componente

```typescript
beforeEach(() => {
  fixture = TestBed.createComponent(MiComponenteComponent);
  component = fixture.componentInstance;
  fixture.detectChanges();
});
```

En esta sección se crea una instancia del componente que se va a probar. `TestBed.createComponent` se encarga de crear el componente embebido en un objeto de prueba. `fixture.componentInstance` es la instancia del componente que se va a probar.

### 4.6. Pruebas

```typescript
it('should create', () => {
  expect(component).toBeTruthy();
});
```

En esta sección se definen las pruebas que se van a realizar. En este caso, se prueba que el componente se haya creado correctamente.

## 5. Ejecución de pruebas
Para ejecutar las pruebas, se debe utilizar el siguiente comando:

```
ng test
```

Este comando ejecutará todas las pruebas que se encuentren en la carpeta ``src/app`` y mostrará los resultados en la consola.

## 6. Ejemplos de pruebas

A continuación, se presentan algunos ejemplos de pruebas que se pueden realizar en un componente:

### 6.1. Prueba de existencia de elementos HTML

```typescript
it('should have an h1 tag with the text "Mi título"', () => {
  const element = fixture.nativeElement.querySelector('h1');
  expect(element.textContent).toContain('Mi título');
});
```

En este ejemplo, se prueba que existe un elemento ``h1`` con el texto "Mi título". ``fixture.nativeElement`` se utiliza para obtener el elemento HTML embebido en el objeto de prueba.

### 6.2. Prueba de cambio de valores

```typescript
it('should increment the value of count when button is clicked', () => {
  const button = fixture.nativeElement.querySelector('button');
  const countBeforeClick = component.count;
  button.click();
  const countAfterClick = component.count;
  expect(countAfterClick).toBeGreaterThan(countBeforeClick);
});
```

En este ejemplo, se prueba que al hacer clic en un botón, se incrementa el valor de una variable count dentro del componente.

### 6.3. Prueba de servicios

```typescript
it('should call the service method on initialization', () => {
  spyOn(service, 'getData').and.returnValue(of({}));
  component.ngOnInit();
  expect(service.getData).toHaveBeenCalled();
});
```

En este ejemplo, se prueba que se llama a un método de un servicio durante la inicialización del componente. ``spyOn`` se utiliza para espiar el método ``getData`` del servicio y ``of({})`` se utiliza para devolver un observable vacío.

## Conclusión

En resumen, realizar pruebas unitarias en Angular es una tarea esencial para asegurar la calidad del código. Con esta guía, los desarrolladores frontend pueden comenzar a realizar pruebas en sus componentes y mejorar la calidad de sus proyectos.

