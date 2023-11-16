# NOTAS REACT
___
react  tiene una sintaxis declarativa, basado en componentes.

crear una appp react con vite usando: 
`yarn create vite`



**Estructura y organizacion de carpetas para react**
```cmd
src/
|- assets/ (para archivos externos: svg, png, ...)
|- components/ (para los componentes de la app)
|- context/ (para los useContext)
|- hooks/ (para los customHOoks)
|- pages/ (para las paginas o ventanas de la app)
|- styles/ (para los estilos)
|- services/ (para servicios,  conexion api, etc)
```

-----------------------------------------------

### HOOKS

#### **_useEffect_**

recive dos parametros
1. una funcion
2. un array

``` javascript
useEffect(()=>{
    //aqui va el codigo que quieres que se ejecute
}, [])
```

la funcion ejecuta la logica segun el caso

caso1: [ ] -> se ejecuta cuando en componente se renderiza por primera vez - componentDidMount

caso2: [stateName] -> solo se ejecuta cuando cambia el estado que estamos agregando

caso3: sin array -> cada que sucede algun cambio en cualquier estado (TENER CUIDADO CON ESTE) - componentDidUpdate


#### **_useRef_**

Este permite hacer una referencia hacia un elemento del DOM, es decir conectar con un elemento especifico


---------------------------------------------

### Hooks Personalizados
Un hooks es una Funcion que recibe algo, y nos devuelve algo

**Creamos una funcion - hook personalizado**
```javascript
export const useName = (parameter)=>{
    //agregamos las instrucciones

    return //retornamos el resultado
    //ojo: tambien es posible retornar un array de valores 
}
```
**Usamos el Hook creado**
```javascript
//imprtamos el hook
import {useName} from '....'

//guardamos la data en una constante
const getData = useNAme(setPArameter);
```
---
### useContext
dentro de la carpeta `context/` añadimos un archivo, y en ahi creamos el contexto.

```javascript
// importamos el hook
import { createContext, useState } from "react";

// lo guardamos en una variable
export const NameContext = createContext();

// creamos un componente 
// este se va encargar de pasar la informacion a los hijos
export const NameContextProvider = ({children})=>{
    //agregamos algo de codigo
    // si lo que usamos es un estado podemos crear un estado global
    const [state, setState] = useState();
    return(
        <NameContext.Provider value={//aqui va el valor que se va actualizar  | {state, setState}}>
            { children }
        </NameContext.Provider>
    )
}
```

para hacer uso del context debemos envolver toda nuestra aplicacion con el provider.

```javascript
import {NamecontextProvider} from '...';

ReactDOM.createRoot(document.getElementById('root')).render(
    <NameContextProvider>
        <RouterProvider router={router}/>
    </NameContextProvider>
)
```

Luego de esto, en el archivo que deseemos importamos nuestro context

```javascript
//importamos el hook de contexto y el context que creamos
import {useContext} from 'react';
import {NameContext} from '...'

export const Component = ()=>{
    // lo almacenamos en una variable
    const variableName = useContext(NameContext);
    return(
        <div>
            <span>{varibleName}</span>
        </div>
    )
}
```

## Formularios React
---

Todos los atributos de las etiquetas en react pasa a tener una estructra camelCase

```javascript
//formulario esrito en react
<form>
    <input type="email" placeholder='Correo Electronico'/>
    <input type="password" placeholder='Contraseña' required/>
    
    <label htmlFor="remenber">Remenber me: 
        <input type="checkbox" name='remenber' id='remenber' defaultChecked/>
    </label>
    
    <textarea name="about" id="about" cols="30" rows="10" defaultValue={'Hola, Sr'}/>

    <select name="country" id="country" defaultValue={''} required>
        <option value="">-Seleccionar-</option>
        <option value="PE">Peru</option>
        <option value="ARG">Argentina</option>
        <option value="BO">Bolibia</option>
        <option value="CHI">Chile</option>
    </select>

    <input type="submit" value="Validar" />
</form>
```

Otra cosa a terner en cuenta en react es que los eventos tambien se van a escribir en camelCase

* onSubmit
* onChange
* onClick
* etc...

```javascript
export function NameComponent() {
  //creamos el manejador de evento
  const handleSubmit = (e)=>{
    //evitamos el comportamiento por defecto
    e.preventDefault();
  }

  return (
    <div>
      <form onSubmit={handleSubmit}>
        //elementos.....
      </form>
    </div>
  )
}
```

### Componentes Controlados
El control total del contenido del input lo maneja el estado y le quitamos la responsabilidad al DOM

```javascript
import { useState } from 'react';

export function Comopnent() {
  //creamos un estado
  const [caracteres, setCaracteres] = useState("");
  //dentro del manejador de cambio actualizamos el valor del estado
  const handleChange = (e)=>{
    setCaracteres(e.target.value);
  }

  return (
    <div className="App">
      <form >
        //agregamos un evento onChange y establecemos el valor como el estado
        <input type="email" placeholder='Correo Electronico'
         onChange={handleChange} value={caracteres} />
        <input type="submit" value="Validar" />
      </form>
    </div>
  )
}
```

haciendo uso del manejo de estados podemos recuperar la data del formulario y guardarla en un objeto

```javascript
import { useState } from 'react';

export function Componente() {
  // creamos una variable con el hook useState
  // y como valor le damos un objeto
  const [caracteres, setCaracteres] = useState({'email': '', 'password': ''});
  
  //en el manejador de cambios recuperamos los valores
  //y actualzamos el estado de la variable
  const handleChange = (e)=>{
    //recuperamos los datos desestructurando la variable
    let {name, value} = e.target;
    //de esta manera le decimos que a nuestra variable previa
    //le cambie solo los valores
    setCaracteres({...caracteres, [name]:value});
  }

  const handleSubmit = (e)=>{
    e.preventDefault();
    console.log(caracteres);
  }

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <div>
          <label htmlFor="email">Email:
            <input type="email" name='email' id='email' 
            onChange={handleChange} value={caracteres.email} autoComplete='off'/>
          </label>
        </div>
        <div>
          <label htmlFor="password">Password:
            <input type="password" name='password' id='password'
             onChange={handleChange} value={caracteres.password} />
          </label>
        </div>
        <div>
          <input type="submit" value="Ingresar" />
        </div>
      </form>
    </div>
  )
}
```

### Componentes Reutilizables

para hacer uso de componentes reutilizables dentro de un formulario hacemos lo siguiente

creamos un `./componentes/input.jsx` 

```javascript
export function Input({type,label,value, handleChange}) {
    return(
        <div>
            <label htmlFor={type}>{label}:
                <input 
                    type={type} 
                    name={type} 
                    id={type} 
                    onChange={handleChange} 
                    value={value} 
                />
            </label>
        </div>
    )
}
```
luego simplenente lo importamos en el formulario que creamos

```javascript
function App() {
  import { Input } from '...';
  /*
   codigo extra...
  */

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <Input type='email' label='Correo Electronico' 
        value={caracteres.email} handleChange={handleChange} />
        <Input type='password' label='Contraseña' 
        value={caracteres.password} handleChange={handleChange}/>
        <div>
          <input ype="submit" value="Ingresar" />
        </div>
      </form>
    </div>
  )
}
```