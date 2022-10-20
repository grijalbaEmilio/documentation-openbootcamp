# TypeScript
TypeScript es un lenguaje de programación con una sintaxis similar a JavaScrip, pero utiliza tipos de datos para que el código sea más escalable y mantenible.
TypeScript transpila el código a javaScript que es el lenguaje que entienden los navegadores o los entornos de ejecución como node.js.

## instalación
    npm install -g typescript

## transpilar ts a js
```
tsc nameFile.ts 
```
``` 
tsc nameFileOne.ts nameFileTwo.ts nameFileTrhee.ts 
```
```
tsc *.ts 
```

## tsconfig.json
configuración que indica de que forma se transpilará a js

iniciar
```
tsc --init
```
propiedades de ejemplo
```json
{
    "compilerOptions": {
        "target": "es2016",// Set the JavaScript language version for emitted JavaScript
        "module": "commonjs", // Specify what module code is generated.
        "outDir": "./build", // Specify an output folder for all emitted files.
        "strict": true, // Enable all strict type-checking options.
    }
}
```

# data Types

básicos
```ts
const decimal: number = 32
const hex: number = 0xF00f
const num: number = 0b1011

const bool: boolean = true
const stringSlice: string = 'hello, world!'
```

## listas - arreglos
```ts
const lst: number[] = [1, 2, 3, 4]
const lst2: Array< number > = [1, 2, 3, 4]
let values: (string | number | boolean) = ["hello, world", 12, true]
```

## tuplas
```ts
const tupleOne: [ number, string ] = [ 21, 'hello, world!' ]
```

## enums
```ts
enum colors{
    red = "red",
    blue = "blue",
    yellow = "yellow"
}

enum Nums{
    "one" = 1,
    "two",
    "three"
}

// use
let num: Nums = Nums.one;
```

## interfaces
```ts
interface User{
    id: strin
    name: string
    age: nuber
    email: string
}

interface Task{
    id: Nums
    name: string
    stage: string
    author: User
}

// use
len oneTask: Task = {
    id: Nums.one,
    name: "one task",
    stage: "important",
    author: {id: 1, name: "juan", age: 29, emal: "uan@gmail.com"}
}
```

## types
```ts
type Product = {
    price: number,
    name: string
}

let car: product = {
    price: 12000,
    name: "BMW"
}

console.log(car.name)
//use
```

## functions
```ts
function myfunction(number: string | undefined, name: string = "no name"): number{
    return 2
}
// equivale a

function myfunction(number?: string, name: string = "no name"): number{
    return 2
}
```
```ts
function sum(...nums: number[]): number{
    return nums.reduce((acc, x) => acc + x, 0)
}
```

```ts
async function sum(...nums: number[]): Promise<number>{
    return await nums.reduce((acc, x) => acc + x, 0)
}
```

función generadora
```ts
function* exampleGnerator(){
    let index = 0

    while(index < 5){
        yield index++;
    }
}

// use
let generator = exampleGenerator()

console.log(generator.next().value); // 0
console.log(generator.next().value); // 1
console.log(generator.next().value); // 2
```

```ts
function* watcher(valor: number){
    
    yield valor
    yield* worker(valor)
    yield valor + 10
    
}

function* worker(valor: number){
    yield vlor + 1
    yield vlor + 2
    yield vlor + 3
}
// use
let generator = exampleGenerator(0)

console.log(generator.next().value); // 0
console.log(generator.next().value); // 1
console.log(generator.next().value); // 2
console.log(generator.next().value); // 3
console.log(generator.next().value); // 10

```

## Clases
```ts
 class Student{
    // property of class
    name: string
    lastname?: string
    private age: int

    //constructor
    constructor (name: string, lastname?:string){
        this.name = name
        if(lastname) this.lastname = lastname
    }

    get name(): string{
        return name
    }

    set age(age: string): void{
        this.age = age
    }
 }
```

## herencia
```ts
 class StudentDB extends Student{
    // content calss
 }
```

## interfaces POO
```ts
 interface ITask{
    title: string,
    description?: string,
    abstract: () => string
 }

// use
class taskU implements ITask{
    title: string,
    description?: string,

    constructor taskU(title: string) {
        this.title = title
    }

    abstract = ():string => {
        return this.title + "final abstract"
    }
}
```

## decoradores -> @

en clases

en parámetros
```ts
// use functions as decorator
function vewPosition(targer: any, propertyKey: string, parameterIndex: number){
    console.log("position: ", parameterIndex);
    
}

// use
class tesOnlyRead{
    
    test(a: string, @vewPosition b: boolean){
        console.log(b);  
    }
}

en métodos

en propiedades
```ts
// use functions as decorator
function onlyRead(targer: any, key: string){
    Object.defineProperty(target, key, {
        writable: false
    })
}

// use
class tesOnlyRead{
    @onliRead
    name: string = 'my name'
}
```