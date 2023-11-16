# Bootstrap

**Menu**
- [Bootstrap](#bootstrap)
  - [Container](#container)
  - [Grid](#grid)
  - [Puntos de Ruptura](#puntos-de-ruptura)
  - [Gutters](#gutters)
  - [Elementos flotantes](#elementos-flotantes)
  - [Display](#display)
  - [Alineacion](#alineacion)

## Container

Los container por lo general se usa para encerrar las grilas de boostrap.

||XS|S|M|L|XL|XXL|
|-|-|-|-|-|-|-|
|.container	|100%	|540px	|720px	|960px	|1140px	|1320px|
|.container-sm	|100%	|540px	|720px	|960px	|1140px	|1320px|
|.container-md	|100%	|100%	|720px	|960px	|1140px	|1320px|
|.container-lg	|100%	|100%	|100%	|960px	|1140px	|1320px|
|.container-xl	|100%	|100%	|100%	|100%	|1140px	|1320px|
|.container-xxl	|100%	|100%	|100%	|100%	|100%	|1320px|
|.container-fluid	|100%	|100%	|100%	|100%	|100%	|100%|

```html
<div class="container-sm">100% wide until small breakpoint</div>
<div class="container-md">100% wide until medium breakpoint</div>
<div class="container-lg">100% wide until large breakpoint</div>
<div class="container-xl">100% wide until extra large breakpoint</div>
<div class="container-xxl">100% wide until extra extra large breakpoint</div>
```

## Grid

para establecer grillas en la pagina se usa **rows** y **cols**

* rows .- son la filas que va tener pagina
* cols .- son las comlumnas que va tener la pagina, por lo general estas van dentro de los rows, el numero de columnas debe sumar maximo 12.

```html
<div class="container text-center">
  <div class="row">
    <div class="col-6">
      Column
    </div>
    <div class="col-3">
      Column
    </div>
    <div class="col-3">
      Column
    </div>
  </div>
</div>
```

## Puntos de Ruptura


|Breakpoint	|Class infix |Dimensions|
|-|-|-|
|Extra small	|None	|<576px|
|Small	|sm	|≥576px|
|Medium	|md	|≥768px|
|Large	|lg	|≥992px|
|Extra large	|xl	|≥1200px|
|Extra extra large	|xxl	|≥1400px|

Los puntos de ruptura permites manejar el diseño responsivo de las paginas, para hacer uso de los "breakpoint", se coloca su nomenclatura en medio de la clase:

```html
<div class="container text-center">
  <div class="row">
    <div class="col-sm-12 col-lg-6">
      Column
    </div>
    <div class="col-sm-12 col-lg-3">
      Column
    </div>
    <div class="col-sm-12 col-lg-3">
      Column
    </div>
  </div>
</div>
```

## Gutters

son el **padding** entre las columnas que permite espaciar y alinear el contenido de las **grid** de bootstrap.

si has trabajado con css sepuede entender como el atributo **gab**

```html
<div class="container text-center">
  <div class="row gx-2 gy-2"><!--se puede simplificar con g-2-->
    <div class="col-6">
      <div class="p-3">Custom column padding</div>
    </div>
    <div class="col-6">
      <div class="p-3">Custom column padding</div>
    </div>
    <div class="col-6">
      <div class="p-3">Custom column padding</div>
    </div>
    <div class="col-6">
      <div class="p-3">Custom column padding</div>
    </div>
  </div>
</div>
```

## Elementos flotantes
* .float-start
* .float-end
* .float-none
* .float-sm-start
* .float-sm-end
* .float-sm-none
* .float-md-start
* .float-md-end
* .float-md-none
* .float-lg-start
* .float-lg-end
* .float-lg-none
* .float-xl-start
* .float-xl-end
* .float-xl-none
* .float-xxl-start
* .float-xxl-end
* .float-xxl-none

## Display

para usar la propiedad display se hace de la siguiente manera:
> .d-{value} for xs<br>
> .d-{breakpoint}-{value} for sm, md, lg, xl, and xxl.

el **value** se puede sustituir por cualquera de estos parametros:

* none
* inline
* inline-block
* block
* grid
* inline-grid
* table
* table-cell
* table-row
* flex
* inline-flex

## Alineacion

La aliacion de elemtos trabaja con los atributos de display flex

* align-items-{value} .- alinea los item de manera vertical
* justify-content-{value} .- alinea los items de manera horizontal

existe una propiedad **offset** que permite crear una especie de elementos imaginaros. 

