### Variaveis
| keyword | desc |
| --- | --- |
| `var` | tem escopo global limitado ao bloco de função mais proximo |
| `let` | tem seu escopo limitado ao bloco em que se encontra |
| `const` | tem escopo similar ao `let` porem seu valor não pode ser alterado|

### Tipos
|  | descrição | primito/não primitivo (objeto) |
| --- | --- | --- |
|String | representa uma sequencia de caracteres ou texto | primitivo
|Number | representa numeros inteiros, float, +Infinity e -Infinity| primitivo | 
|Boolean| representa valores resultantes de condicionais (verdadeiro/falso) | primitivo|
|Symbol| representa um valor simbolico unico mesmo que os valores reais sejam iguais | primitivo |
|Bigint | representa valores grandes onde o valor é maior que `Number.MAX_SAFE_INTEGER` | primitivo |
|null| representa a ausencia de valor | primitivo |
|undefined | representa a ausencia de declaração | primitivo |
| Object | representa um objeto com coleção de valores chave e valor similiar a um map | não primitivo |
| Array | representa uma coleção de valores | não primitivo |
| Function | bloco de codigo isolado que pode ser invocado programaticamente | não primitivo |
| Date | representa valores de datas | não primitivo |

### Operadores
| | |
| --- | --- |
| % | resto da divisão |
| * | multiplicação |
| / | divisão |
| + | soma |
| - | subitração |
| = | atribuição |
| == | comparador de igualdade sem considerar tipo |
| === | comparador de igualdade considerando o tipo |
| ! | negação |
| && | operador 'e' |
| \|\| | operador 'ou' |

### Loops
```js
// for comum
for (let i = 0; i < 10; i++){
    console.log(i);
}

// for in
for (let index in someArray){
    console.log(index);
}

// for of
for (item in someArray){
    console.log(item);
}
```

### Funções
#### `Funções declarativas`
São funções definidas com a keyword `function` que recebem um determinado nome.
```js
function declarativeFunc(){
    console.log('this is a declarative function!');
}
```
#### `Expressões de função`
São funções definidas por associação.
```js
const expressionFunc = function () {
    console.log('this is an expression function!');
}
```
A principal diferença nessa abordagem é como elas são afetadas pelo `hoisting`.

#### `Funções construtoras`
As funções contrutoras são funções que ao serem chamadas com o `new`
é criado um objeto vazio e o valor da propriedade `prototype` da função construtora é atribuido ao novo objeto e executa a função construtora vinculando o contexto com o contexto do novo objeto criado.
```js
function ContructorFunc(){
    this.attribute = 100;
}

const instance = new ConstructorFunct(); // ConstructorFunc {"attribute": 1000}
```

#### `.call` e `.apply`
Os metodos call e apply permitem executar funções explicitamente com contextos especificos.
```js
function greet(greeting, punctuation) {
    console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: "Alice" };
greet.call(person, "Hello", "!");
greet.apply(person, ["Hello", "!"]);
```

#### `first class function` e `high order function`
`first class function` Refere-se à capacidade de tratar funções como valores.
```js
const sqrt = function (value){
    return value * value;
}
const cbrt = function (value){
    return value * value * value;
}
function potence(value, method){
    console.log(method(value));

const methods = [sqrt, cbrt];
methods.forEach(method => potence(2, method)); // 4, 8
```
`high order function` São funções que recebem ou retornam outras funções.
```js
function makePowerFunction(exponent) {
    return function(base) {
        return Math.pow(base, exponent);
    };
}

const square = makePowerFunction(2);
const cube = makePowerFunction(3);

console.log(square(4)); // Output: 16
console.log(cube(4));   // Output: 64
```

### Orientação a protótipo
A orientação a prototipo no JS é uma forma de herança entre objetos.
```js
const clothes = {sizes: ['p', 'm', 'g']}

const tShirt = {
    color: 'blue',
    __proto__: clothes,
}

console.log(tShirt.sizes); // ['p', 'm', 'g']


function ConstructorFunc(){
    this.attr = 100;
}
ConstructorFunc.prototype.method = function(){
    console.log(this.attr);
}
const instance = new ConstructorFunc();
instance.method();
```

### Classes
As classes no js são um forma de açucar sintatico para as funções construtoras.
```js
// isso
class Person {
    constructor (name) {
        this._name = name;
    }

    sayHi(){
        console.log(`Hi ${this._name}`);
    }

    get name(){ // equivale a uma property do python
        return this._name;
    }
    set name(value) { // equivale a um setter no python
        this._name = value
    }
}

// é equivalente a isso
function PersonFunc(name){
    this.name = name;
}
PersonFunc.prototype.sayHi = function (){
    console.log(`Hi ${this.name}`);
}
```

### Objetos literais
Os objetos literais são muito parecidos com o `dict` no python com algumas peculiariedades.
```js
let person = {
    name: 'Jhon Doe',
    age: 21,

    sayHello: function () {
        console.log(`hello ${this.name}!`);
    }
}

console.log(person.name);
console.log(person['age']);

person.sayHello();
```

### Promises
As Promises são uma forma de trabalhar com eventos assincronos
```js
const asyncEvent = new Promise((resolve, reject) => {
    let ok = true;
    // some processing
    ok ? resolve() : reject('something went wrong!')
});

asyncEvent
    .then((result) => {/*...*/})
    .catch((error) => {/*...*/})
    .finally(() => {/*...*/})
```

### Async/Await
A interface async/await é um açucar sintatico para as promises, possibilitando a utilização em um formato similar a programação sincrona.
```js
async function fetchData(){
    try {
        response = await fetch('https://example.com/');
        return await response.json();
    } catch (error) {
        // ...
    } finally {
        // ...
    }
}
```

### `Spread operator` e `Object destructuring`
```js
// O spread é similar ao unpaking do python desempacotando os valores
let array1 = [1, 2, 3];
let array2 = [4, 5, 6];

newArray = [...array1, ...array2]; // [ 1, 2, 3, 4, 5, 6 ]

// o object destructuring é similar porem com objetos
// a diferença é que vc pega o valor apartir do nome da chave
const someObject = {key1: 'valor1'};
const { key1 } = someObject;

console.log(key1) // valor1
```

### Imports
Para fazer imports no js é preciso antes fazer o `export`
```js
// utils.js
function myFunction(something){
    // do something
}

export { myFunction };

// main.js
import { myFunction } from './utils.js';

myFunction('something');
```
no arquivo html o modulo `utils.js` de ser uma tag `script` com o `type=module`.

### Condicionais
```js
// simples
if (condition) {
    // do something
} else if (otherCondition) {
    // do something else
} else {
    // ...
}

// ternária
condition ? 'isTrue' : 'isFalse';
```

### fetch
O fetch é um metodo nativo do java script que possibilita realizar requisições http e retorna uma promise
```js
// por default a requisição é um GET
fetch(url)
    .then(function (response){
        // do something
    })
    .catch(function (error){
        // do something
    })
    .finally(function (){
        // ...
    })

// usando encadeamento de then
fetch(url)
    .then(function (response){
        return response.json();
    })
    .then(function (json_data){
        // do something with the return of the first .then
    })
    .catch(function (error){
        // do something
    })
    .finally(function (){
        // ...
    })

// usando arrow functions
fetch(url)
    .then((response) => return response.json();)
    .then(function (json_data){
        // do something with the return of the first .then
    })
    .catch(function (error){
        // do something
    })
    .finally(function (){
        // ...
    })

// utilizando outros metodos
fetch(url, {
    method: 'POST',
    headers: {
        token: 'Bearer 123'
    },
    body: {
        test: '123',
    }
}).then((response) => console.log(response.status == 201 ? 'success' : 'fail'));
```