# Programacion Orientada a Objetos

## Objetos Literales
```javascript
//creamos un objeto literal
const alumno = {
    //creaos los atributos
    nombre: "Denilon",
    Apellidos: "Salas Guzman",
    edad: "24",
    //creamos un metodo
    presentarse(){
        console.log(`Hola, mi nombre es ${this.nombre}`);
    }
}
//modificamos el atributo nombre
alumno.nombre = "Denilson Luciano"
//agregamos un nuevo atributo
alumno.genero = "Masculino"
//imprimimos el objeto
console.log(alumno);
//Llamamos al metodo presentarse 
alumno.presentarse();
```
**_salida_**
```cmd
{
  nombre: 'Denilson Luciano',
  Apellidos: 'Salas Guzman',
  edad: '24',
  presentarse: [Function: presentarse],
  genero: 'Masculino'
}
Hola, mi nombre es Denilson Luciano
```

## Funcion Constructora
```javascript
function Usuario(nombre, edad, email) {
    this.nombre = nombre,
    this.edad = edad,
    this.correo = email
}

const Denilson = new Usuario('Denilson', 24, 'dlsg@gmail.com')
const Mikhail = new Usuario('Mikhail', 14, 'msg@gmail.com')
```

**_salida_**
```cmd
Usuario { nombre: 'Denilson', edad: 24, correo: 'dlsg@gmail.com' }
Usuario { nombre: 'Mikhail', edad: 14, correo: 'msg@gmail.com' }
```

## Clases
```javascript
class Usuario{
    //el metodo contructor contiene los atributos
    constructor(nombre, edad, email){
        this.nombre = nombre,
        this.edad = edad,
        this.correo = email
    }
    //creamos un metodo para nuestra clase usuario
    presentarse(){
        //una buena practica es no usar el clg para imprimir los mesajes
        const message = `\nHola,\nsoy ${this.nombre},\nmi correo es ${this.correo}`;

        return message
    }
}
//Creamos las instancias de los objetos
const denilson = new Usuario('Denilson', 24, 'dlsg@gmail.com')
/*
 * una instancia es un objeto creado a partir de una clase
*/
//imprimimos el nuevo objeto
console.log(denilson)
//invocamos al metodo del objeto
console.log(denilson.presentarse())
```

**_salida_**
```cmd
Usuario { nombre: 'Denilson', edad: 24, correo: 'dlsg@gmail.com' }

Hola,
soy Denilson,
mi correo es dlsg@gmail.com
```
### Métodos getters y los setters

```javascript
class Usuario{
    /*
    * codigo anterior ...
    */

    //se usan para conservar las buenas practicas 
    // GET -> Obtener datos de la clase
    getNombre() {
        return this.nombre
    }
    // SET -> Dar nuevos datos a la clase
    setNombre(nuevoNombre) {
        this.nombre= nuevoNombre
    }
}
//Creamos las instancias de los objetos
const denilson = new Usuario('Denilson', 24, 'dlsg@gmail.com')
//invocamos al metodo get y set
console.log('antes: '+ denilson.getNombre())
denilson.setNombre('Denilson Luciano')
console.log('despues: '+ denilson.getNombre())
```

**_salida_**
```cmd
antes: Denilson
despues: Denilson Luciano
```

### Herencia
Clase padre - usuario
```javascript
class Usuario{
    constructor(nombre, edad, email){
        this.nombre = nombre,
        this.edad = edad,
        this.correo = email
    }
    presentarse(){
        const message = `Hola,\nsoy ${this.nombre}, mi correo es ${this.correo}.`;

        return message
    }
}
```
Clase hijo - profesor
```javascript
class Profesor extends Usuario{
    constructor(nombre, edad, email, cursosDictados){
        super(nombre, edad, email)
        this.cursosDictados = cursosDictados
    }
    CursosDictados(){
        const message = `Los cursos que dicto son ${this.cursosDictados}`
        return message
    }
}
//Creamos las instancias de Profesor
const denilson = new Profesor('Denilson', 24, 'dlsg@gmail.com',["html", "css", "JS"])
console.log(denilson.presentarse());
console.log(denilson.CursosDictados())
```
Clase hijo - alumno
```javascript
class Alumno extends Usuario{
    constructor(nombre, edad, email, cursosTomados){
        super(nombre, edad, email)
        this.cursosTomados = cursosTomados
    }
    CursosTomados(){
        const message = `Los cursos que he hecho son ${this.cursosTomados}`
        return message
    }
}
//Creamos las instancias de Alumno
const Mikhail = new Alumno('Mikhail', 14, 'msg@gmail.com',["html", "css", "Figma"])
console.log(Mikhail.presentarse());
console.log(Mikhail.CursosTomados())
```
**_salida_**
```cmd
Hola,
soy Denilson, mi correo es dlsg@gmail.com.
Los cursos que dicto son html,css,JS
Hola,
soy Mikhail, mi correo es msg@gmail.com.
Los cursos que he hecho son html,css,Figma
```