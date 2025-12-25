# Nc Programming Language

Nc programming language or informally called NPL is a next generation invasive constraint based strongly typed memory safe programming language that aims to redefine the programming space by incorporating any and all current technologies in the programming space while also making it possible to easily integrate future technologies with its robust design.

It is a language that is designed from its infancy to accommodate every known area of programming and also, importantly, make a programmer's experience near equal or comparable to programming languages specifically designed for those known areas. The language does this by centralizing specific functionalities of those areas of programming thereby making itself aware of the various programming areas then dictates when a programmer can use said functionalities. An example of said functionality would be using the programming language as a low and high level systems programming language, mobile systems programming language, **GUI** programming language, web programming language, game design programming language, embedded systems programming language, scripting programming language and many more(Although it cannot be used as a data language, that is **JSON** or **XML**, nc data representation language already serves such purpose and is natively integrated in nc programming language).

It is essentially an programming area aware language and it is for this reason I call the language a **TGPL**(Truly General Purpose Programming Language).

## Nc Programming Language Features

The following describes some of the many features of the nc programming language:

- Positional base number entry from bases 2 to 36 (For both integer and real numbers)
- Raw user identifier entry
  - Raw user language identifier entry
  - Raw user string identifier entry
- Discard and document comments
- Character entry
- Multi-line string entry
- Embedded raw strings
- Text action entry (Known as escape sequences in C, C++ and most other programming languages)
- High width integers up to 512-bytes or 4096-bits
- Platform integers
- IEEE-745 binary floating point numbers (Reluctantly added)
- Nc real numbers (A custom decimal floating point implementation native to the language)
- Strongly typed language
- No implicit conversions and no sub-typing
- Highly expressive type system
- Stack array type(An array data structure that only uses the stack memory space invented just for the language)
- Static array type
- Integer range types
- Failure handling types
- Zero sized types
- Product type creators (Similar to structs in C and Rust)
- Sum type creators (Similar to enums in Rust and unions in C and C++)
- Semantic type creators (Similar to derived types in Ada but with added semantics)
- Semantic ranged integer type creators (Similar to Integers in Ada)
- Value definition type creators (Similar to enum classes in C++)
- Value semantics:
  - Move value semantics (Destructive move semantics)
  - Copy value semantics
- Functions
- Marcos (Inlined functions devoid of value semantics)
- Objects (Known as variables in various programming languages)
- Objects are immutable by default
- Circular dependency resolution for object initialization in the global space
- Thread local objects
- Loops:
  - For iterator loop (Similar to for loops in the Rust programming language)
  - While loop (Similar to for loops in the C and C++ programming languages)
- Interfaces via Contract and impl (Similar to trait and impls in Rust)
- Language defined generic unicode string interface that supports extensive unicode functionalities
- Robust compile time evaluation semantics
- Explicit and implicit default value argument entry
- Value argument list generators (Allows value list generation in any value argument entry)
- Access restriction semantics (Controls the visibility of language items)
- Import system
- Compile time polymorphism:
  - Type parameters (parametric polymorphism in programming or colloquially known as generics) that support generic typing
    - Type constructor type parameter (Similar in concept to Higher Kinded Types in Haskell but limited in semantics to keep it simple)
  - Compile time value parameters (Basically the value parameter version of type parameters, can be seen in parametric polymorphism implementation in languages like Rust and C++)
- Run time polymorphism:
  - Contract types (Basically impl types in Rust but with a significantly different implementation)
- Groupings (Pinnacle of less typing and semantic syntax grouping in a high level context)
- Variadics (Similar in concept to paramter packs in C++)
- Tuples and variants (Basically anonymous product and sum types enabled by the variadics feature)
- Language communication interface (**LCI**):
  - Attribute LCI (Includes the various language constraints and many more)
  - Expression LCI (Exposes interfaces to language metadata and special language functions)
  - Type LCI (Exposes interfaces to language type system metadata)
  - Miscellaneous LCI (Involves unrelated special language functionality)
- Constraint application (Allows the entry of user defined constraint on various language items)
- Unified function call (**UFC**)
- Redefined precedence for various operators
- Limited operator overloading
- Operator combinations (Allows for chaining certain operators)
- Collection expressions
- Literal tags (Known as literal types in C++)
- Custom collection expression definition
- Custom literal tag definition
- Blocks as expressions
- Conditional expressions:
  - If conditional expression
  - Match condtional expression
  - Or-field query conditional expression (A more robust form of pattern matching expression in functional languages and Rust)
- References:
  - Value references (Similar in concept to references in C++ and Rust)
    - Non allocating value references
    - Allocating value references
  - Memory address references (Similar in concept to pointers in C and C++):
    - Non allocating memory address references
    - Allocating memory address references
- Implicit lifetime semantics (Similar in concept to explicit lifetime parameters in rust)
- Scope definitions (Similar in concept to namespaces in C++)
- Type creator introspection
- Value unpacking (Similar to structured binding in C++ but way more expressive and robust)
- 1-based indexing (Subjectively better than 0-based indexing for me)
- Foreign interface
- Platform agnostic computing
- Whitespace decisive synparsing
- Well defined language semantics
- Excellent compiler error messages called error logs

## Nc Programming Language Examples

Due to NPL not having syntax highlighting yet in the code format section of markdown, the rust programming language is selected as the programming language to use its syntax highlighting because it is the only language included that remotely resembles NPL syntax, therefore enables the syntax highlighting of a few. It is for this same reason that NPL discard and document single-line comment contents (`>!` & `>:`)  are enclosed with double quotes to prevent syntax highlighting, since the comments syntax are different than rust's.

- Hello world example

```rust
import marco std:print

fn main {
    print("Hello World(from nc programming language)")
}
```

- Raw user string identifier and raw language identifier entry example

```rust
fn main {
    obj _ r"Do you love 🧸s?" = true
    obj _ r:for = "Damn! using the `for` language identifier as a user identifier"
    obj _ r"Are you an ape(🦍)?" = true
    obj _ r:struct = "Wow! using the `struct` language identifier as a user identifier"
}
```

- References example

```rust
import type std:alloc:basic

fn main {
    obj a: ui4()
    
    value_ref(&a, mut&a)
    memory_address_ref(addressof a, mut addressof a)
    
    alloc_value_ref(obj: allocator:basic[ui4].allocate())
    alloc_memory_address_ref(obj: allocator:basic[ui4].allocate())
}

fn value_ref(obj _: &ui4, obj _: mut&ui4) {}
fn memory_address_ref(obj _: *ui4, obj _: mut*ui4) {}

fn alloc_value_ref(obj alloc: {&}ui4) {
    obj: allocator:basic[ui4].deallocate(alloc)
}
fn alloc_memory_address_ref(obj alloc: {*}ui4) {
    obj: allocator:basic[ui4].deallocate(alloc)
}
```

- Sum type creator example

```rust
import type std:string
import marco std:printf

union realNumber = obj (real4: r4, real8: real8)

fn main {
    obj realNum: realNumber()
    
    realNum => real4 {
        printf("$(real4)=\n")
    }|real8 {
        printf("$(real8)=\n")
    }
}
```

- Value Unpacking examples

```rust
import type std:string
import marco std:printf

struct product = obj (name: string, id: ui8, amount: ui4)

scope @product =
>! "The parameter uses value unpacking"
fn display(obj {name, id, amount}: &product) {
    printf("\
    		Product name	= [$(name)]\
        	Product id		= [$(id)]\
        	Product amount	= [$(amount)]\n\
    ")
}
end scope

fn main {
    obj bicycle: product("Bicycle", 100₂₈, 102)
    
    &bicycle.display()
}

>! "Value unpacking can also be applied to and-fields(objects in struct) and normal objects too"
```

- Contract and impl with runtime polymorhism example

```rust
import marco std:printf

contract[type Self] animal =
fn sound(obj self: &Self) &str;
fn name(obj self: &Self) &str;
end

struct (dog, cat);

scope @dog =
impl[dog] animal =
fn sound(obj _: &Self) &str {
    "woof"
}

fn name(obj _: &Self) &str {
    "Dog"
}
end
end scope

scope @cat =
impl[cat] animal =
fn sound(obj _: &Self) &str {
    "meow"
}

fn name(obj _: &Self) &str {
    "Cat"
}
end
end scope

fn animal_sound(obj animal: !animal) {
    printf("$(animal.name())s makes this sound $(animal.sound())")
}

fn main {
    obj (dog: dog(), cat: cat())
    
    animal_sound(dog)
    animal_sound(cat)
}
```

- Constraint application and compile time polymorphism using type parameters example

```rust
import type std:string

marco add[type T](obj (lhs, rhs): T) T apply @T eq string or eq @ui4 {
    lhs + rhs
}

fn main {
    obj _ = add(34, 45) >! "result = `79`"
    obj _ = add(string"Daniel", string" Emeka") >! "result = `Daniel Emeka`"
}
```

- Variadics for functions and constraint application example

```rust
fn sum(obj ..args: ui4) ui4 apply variadics(args).size gt 2 {
    obj result: ui4()
    
    for arg in variadics(args) {
        result += arg
    }
    
    result
}

import marco std:printf

fn main {
    obj sum = sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    
    printf("$(sum)=") >! "Prints `sum = 55`"
}
```

- Type constructors example

```rust
>! "Haskell functor: fmap :: f a -> (a -> b) -> f b"
contract[type Self[?]] functor[type A] =
fn fmap[type (B, Fn)](obj (self: Self[A], fcn: Fn)) Self[B] apply @Fn impls fn(A)B;
end

import type std:(arrayList, maybe)

>! "Type constructor arrayList implementing functors"
scope @arrayList[type T] =
impl[arrayList] functor[T] =
fn fmap[type (B, Fn)](obj (self: arrayList[T], fcn: Fn)) Self[B] apply _ {
    self.map(fcn)
}
end
end scope

>! "Type constructor maybe implementing functors"
scope @maybe[type T] =
impl[maybe] functor[T] =
fn fmap[type (B, Fn)](obj (self: maybe[T], fcn: Fn)) Self[B] apply _ {
    self => some {
        obj: maybe(some)
    }else
}
end
end scope

fn do_something[type (T, U)](obj x: T) U apply @T impls functor[ui4] {
    x.fmap(fn(obj n){ -> n.to_string(.base= 21) })
}

fn main {
    obj maybe_age: maybe(56)
    obj age_list = arrayList[21, 34, 56, 34, 23, 8]
    
    do_something(maybe_age)
    do_something(age_list)
}
```

- Value argument list generators, collection expressions and static arrays example

```rust
import marco std:printf

fn main {
    obj static_array: arr[ui4]!(1024)
    
    >! "Delay initialization "
    static_array := arr[->> for x in 1~1024 {x + 3}]
    
    >! "Essentially results in `arr[1+3, 2+3, 3+3, ..., 1024+3]`"
}
```

- Matrix and vector implementation using static arrays and collection expressions example

```rust
import marco std:printf

fn main {
    >! "Matrix"
    obj _ = obj: matrix([[3.0, 4.0], [3.0, 4.0]]) >! "Using object constructors"
    obj _ = matrix[[3.0, 4.0], [3.0, 4.0]] >! "Using collection expressions"
    
    >! "Vector"
    obj _ = obj: vector([2.0, 3.0]) >! "Using object constructors (2d vectors)"
    obj _ = vector[2.0, 3.0] >! "Using collection expressions (2d vectors)"
    
    obj vec3d_add_result = vector[2.0, 3.0, 9.0] + vector[5.0, 6.0, 1.0]
    obj vec2d_add_result = vector[4.6, 9.1] + vector[3.0, 1.0]
    
    printf("$(vec3d_add_result)=\n") >! "Prints `vec3d_add_result = [7.0, 9.0, 10.0]`"
    printf("$(vec2d_add_result)=\n") >! "Prints `vec2d_add_result = [7.6, 10.1]`"
    
    obj _ = vector2d_request(vector[3.9, 0.5])
    obj _ = vector3d_request(vector[5.9, 5.9, 2.0])
    
    fn vector2d_request(obj x: vector!(2)) {
        printf("Request 2d vector $(x.[1])= & $(x.[2])=\n")
        >! "Prints `Request 2d vector x = {} & y = {}`"
    }
    fn vector3d_request(obj x: vector!(3)) {
        printf("Request 2d vector $(x.[1])= & $(x.[2])=\n")
        >! "Prints `Request 2d vector x = {} & y = {}`"
    }
}

<'------------------------matrix------------------------'>
unique matrix!(obj (row, column): ui) = arr[
    arr[r4]!(column)
]!(row)

scope @matrix!(obj (row, column): ui) =
marco 'collectionExp(matrix) (obj ..args: arr[r4]!(column)) matrix!(variadic(args).size, column) {
    obj: matrix(['at:unpack args])
}
end scope

<'------------------------vector------------------------'>
>! "A vector implementation that supports only 2 and 3 dimensions haha"

unique vector!(obj dimensions: ui) apply dimensions eq 2 or eq 3 = arr[r4]!(dimensions)

scope @vector!(obj dimensions: ui) =
marco misc:collectionExp(vector) (obj ..args: r4) vector!(variadic(args).size) apply variadic(args).size eq 2 or eq 3 {
    obj: vector(['at:unpack args])
}

marco misc:operator+(obj (lhs, rhs): vector!(dimensions)) vector!(dimensions) {
    >! "Using value argument list generator entry(->>)"
    obj: vector(->> for i in 1~dimensions { lhs.[i] + rhs.[i] })
}

>! "The `use` keyword imports type properties of the uniqued type which is a static array in this case"
use marco misc:operator.[] >! "For (1-based)indexing"
use impl display >! "For printing values in a displayable format"

end scope
```

- Run time type introspection example

```rust
import marco std:printf

fn main {
	obj person_struct = exp:getTypeCreatorMetadata[person, array]()

    printf("TypeCreator [$(person_struct.kind)]\nType [$(person_struct.typeName)]\n")
    
    person_struct => fieldInfoList {
        obj fieldInfoListIter = &fieldInfoList.iter()

        >! "Extract the first element out of the iterator"
        fieldInfoListIter.next() => some(fieldInfo) {
        	printf("AndFields [$(fieldInfo)")
        }else {}
        
        for fieldInfo in fieldInfoListIter {
            printf(", $(fieldInfo)")
        }
        printf("]\n")
    }else {}
    
    >! "Prints:" 
    >! "TypeCreator [struct]"
    >! "Type [person]"
    >! "AndFields [name:&str, age:ui1, location:location]"
}

struct person = obj (name: &str, age: ui1, location: location)
struct location = obj (longitude, latitude): r4
```