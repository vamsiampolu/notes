**Tcomb: A mathemetician's view on programming**

**Jargon**

|Name|Definition|
|:----------:|:------------------------:|
|Set|well defined, collection of distinct objects,all the elements of a set are immutable|
|Domain|a Set of permitted inputs to a function|
|CoDomain|a Set of permitted outputs for a function|
|Function|a relation between a domain and a codomain such that for each input a in the domain maps to only one output b in the codomain|
|SubType |a set B is considered a subtype of A if all elements in B are members of A|
|Chareterstic Function|A definition informing one of whether an element of a type B are members of a type A|
|Type Combinator|a function which accepts existing types as its domain and returns new types as its output|
|Cartesian product|a mathemetical operation on sets A and B represents by A X B  that returns a set of ordered pairs (a,b) where a belongs to A and b belongs to B|

---

In JS, a Set is represented by a function that acts as an identity if the value is the value
is part of the Set and throw a TypeError if it is not.

If an input to a function does not belong to a domain, the function must fail with a `TypeError`

If one cannot figure out what the domain and the codomain are for a function, it is a codesmell

A hash is another mechanism for defining a function where each value on the left represents the domain and each value on the right represents a codomain.

arguments can be considered a `tuple`. it is the same thing to have `n` different arguments as a tuple or a single argument as a struct.

`Object.freeze` is a function that allows an object to be made immutable because:

 _ it does not allow properties to be added to an object

 _ it does not allow properties to be removed from an object

 _ it does not allow the `writable`, `enumerable` and `configurable` properties from being changed.


> `Object.freeze` works best when used in `strict mode`

---

**Primitve Types**

```
const assert = (guard) => {
  if(guard !== true) {
    throw new TypeError()
  }
}

const Nil = x => {
  if(assert(x === null || x === undefined)) {
    return x
  }
}

const Str = x => {
  if(assert(typeof x === 'string')) {
    return x
  }
}

const Num = x => {
  if(assert(typeof x === 'number' && isFinite(x) && !isNaN(x))) {
    return x
  }
}

const Bool = x => {
  if(assert(x === true || x === false)) {
    return true
  }
}
```

---

**SubType**

To define a subtype, first create a charecterstic function:

```

const isPositive = x => x > 0

const subType = (B,isA) => b => {
  b = B(b)
  assert(isA(b))
  return b
}


const Positive = subType(isPostive,Num)
```

---

**Enum**


An enum is a special subtype where the domain is a string and the codomain is a string.
The charecterstic function is a check to see if a property exists on a hash

> all keys to an object are coerced internally to strings regardless of how they are specified.

I think some of these functions would be more readable with currying.


```
const enum = map => subType(Str, s => map.hasOwnProperty(s))

const f = {
  left:true,
  center:true,
  right:true,
  justify:true
}

const CSSTextAlign = enums(f)

CSSTextAlign('up') // throws a TypeError
CSSTextAlign('right') // 'right'
```


---

**Tuples and Structs**

Tuples and Structs are cartesian products, a tuple is accessed by index and a struct is accessed by name.

To convert a `struct` to a `tuple`, one could define a function that looks like this:

```

//struct
{
  name:'Guilo Canti',
  age:40,
  isSingle:true
}

//tuple
['Guilo Canti',40,true]


//function that converts a struct to a tuple
{
  name:0,
  age:1,
  isSingle:2
}
```

The Tuple Type Combinator:

```
'use strict'
const Tuple = types => arr => {
  assert(Array.isArray(arr))
  return Object.freeze(arr.map((el,i) => types[i](el)))
}

const Person = Tuple([Str,Num,Bool])
Person('Guilo Canti',40,true)
```

The Struct Type Combinator:

```
'use strict'
function isObject(x) {
  return typeof x === 'object' && x != null && !Array.isArray(x)
}

function struct(props) {
  return function Struct(props) {
    if(obj instanceof Struct) {
      return obj
    }
    if(!(this instanceof Struct)) {
      return new Struct(obj)
    }

    assert(isObject(obj))
    var ret = {}
    for(var name in props) {
      if(props.hasOwnProperty(name)) {
        var type = props[name]
        ret[name] = type(obj[name])
      }
      return Object.freeze(name)
    }
  }
}


Person = struct({
  name:Str,
  age:Num,
  isSingle:Bool
})
```

---

Combining the types defined so far:

```
var Country = enums({
  Italy:true,
  US:true
})

var Gender = enums({
  Male:true,
  Female:true
})

var Body = tuple([Num,Num])

var Person = {
  name:Str,
  age:Num,
  country:Country,
  gender:Gender.
  body:Body
}

function getBMI(height, weight) {
  return weight/Math.pow(height/100,2)
}

function isFavourable(body) {
  var bmi = getBMI(body[0],body[1])
  return bmi >= 18.5 && bmi <= 25
}

var Climber = subtype(Person,function(p){
  return isFavourable(p.body)
})

var guilo = Climber({
  name:'Guilo',
  gender:'Male',
  country:'Italy',
  body:[178,65]
})
```
