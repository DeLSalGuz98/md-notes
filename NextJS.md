# Next JS
---

Genera sitios estaticos a partir de informacion dinamica.

para iniciar un projecto next usamos el siguiente comando `npx create-next-app@latest` y para correr el proyecto usamos `npm run dev`

```javascript
//creamos una funcion de lo que va renderizar
//este compoente va a recibir unas props
export default function Service({service}) {
    //devuelve el resultado html de lo que se renderiza
    return(
        <div>
            <h2> {service.name} </h2>
            <p>
                {service.detail}
            </p>
        </div>
    )
}
```

```javascript
//para obtener informacion de una API usamos la siguiente funcion
//en este caso las props que recive es del contexto de la url
export const getStaticProps = async (context) =>{
    //del contexto extraemos los parametros
    const {id} = context.params;
    //hacemos la peticion a la API
    const res = await fetch(`http://localhost:3050/services/${id}`);
    //guardamos la data y lo convertimos a JSON
    const service = await res.json();
    //devolvemos las props
    return{
        props:{
            //de preferencia usamos el nombre que de asignamos en el componente
            service  
        },
        //usamos esto para que verifique la BD segun el tiempo establecido en milisegundos
        revalidate: 20 
    }
}
```
```javascript
//a diferencia del anterior este mantiene una peticio constante cada que recarga la pagina
export const getServerSideProps = async (context) =>{
    const {id} = context.params
    const res = await fetch(`http://localhost:3050/services/${id}`);
    const service = await res.json();
    return{
        props:{
            service  
        }
    }
}
```

```javascript
//cuando queremos recibir parametros por la url 
//debemos indicar el numero de rutas dinamicas que debemos renderizar
export const getStaticPaths = async ()=>{
    return{
        paths: [
            {params:{id:'1'}},
            {params:{id:'2'}},
            {params:{id:'3'}}
        ],
        fallback: false
    }
}
```