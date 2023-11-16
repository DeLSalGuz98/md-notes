# Go Lang
---
Lenguaje compilado, esteticamente tipado

estructura basica de archivo go

para correr un archivo go usamos el siguiente comando `go run nombreArchivo.go` 

```go
//nombre del paquete al que pertenece el archivo
package main

//importamos otros paquetes
import {
    "fmt"
}

//es la funcion pricipal
func main(){
    //hacemos uso del paquete importado
    fmt.Println("Hellow wolrd")
}
```

#### Formas de declarar una variable

```go
func main() {
    //forma 1
    var dog string = "gran danes"

    //forma 2
    var dog = "gran danes"

    //forma 3
    dog := "gran danes" 

	fmt.Println(dog)
}
```

para crear una constante usamos la palabra reservada `const`.