# Nc Programming Language

Nc programming language or informally called NPL is an invasive constraint based, strongly typed, memory safe, platform aware, next generation programming language that aims to redefine the programming space by incorporating any and all current technologies in the programming space while also making it possible to easily integrate future technologies with its robust design.

It is a programming language designed from its infancy to accommodate every known area of programming and also more importantly, make a programmer's experience equal to, comparable or better than programming languages specifically designed for those areas. The language does this by centralizing specific functionalities of those programming areas thereby making itself aware of the various areas then dictates when a programmer can use said functionalities based on its settings, the programming areas are referred to as platforms in NPL. An example of said feature would be using the programming language as a low and high level systems programming language, mobile systems programming language, **GUI** programming language, web programming language, game design programming language, embedded systems programming language, scripting programming language and many more (_although it cannot be used as a data language, that is the use cases of **JSON**, **XML** or **TOML**, nc data representation language already serves such purpose and is natively integrated in NPL_).

It is basically a platform (_programming area_) aware programming language and it is for this reason I call the programming language a **TGPL** (_Truly General Purpose Programming Language_), but it is a term it has to earn by its actions not words.

## My Naivete (31/12/2025)

The above insanely ambitious goal of the programming language implies a gross naivete on my part, as of the time of writing this document, I am the sole contributor to this project, I have no big company or community backing, I have no financing and my knowledge of the general programming space needed to implement the platform (*programming area*) aware feature is minuscule, abstract and laughable at best. So, take what you read here with a grain of salt till you see real application software written in the programming language and some form of adoption from the programming community.

## Nc Programming Language Features

The following describes some of the many features of the nc programming language:

- Positional base number entry from bases 2 to 36 (_for both integer and real numbers_)
- Raw user identifier entry
  - Raw user language identifier entry
  - Raw user string identifier entry
- Discard and document comments
- Character entry
- Multi-line string entry
- Embedded raw strings
- Text action entry (_known as escape sequences in C, C++ and most other programming languages_)
- High width integers up to 512-bytes or 4096-bits
- Platform integers
- IEEE-745 binary floating point numbers (*reluctantly added*)
- Nc real numbers (*a custom decimal floating point implementation native to the language*)
- Strongly typing
- No implicit conversions and no sub-typing
- Highly expressive type system
- Stack array type (_an array data structure that only uses the stack memory space invented just for the language_)
- Static array type
- Integer range types
- Failure handling types
- Zero sized types
- Product type creators (*similar to structs in C and Rust*)
- Sum type creators (*similar to enums in Rust and unions in C and C++*)
- Semantic type creators (_similar to derived types in Ada but with added semantics_)
- Semantic ranged integer type creators (*similar to Integers in Ada*)
- Value definition type creators (*similar to enum classes in C++*)
- Value semantics:
  - Move value semantics (*flexible destructive move semantics*)
  - Copy value semantics
- Functions
- Marcos (*Inlined functions devoid of value semantics*)
- Objects (*known as variables in various programming languages*)
- Objects are immutable by default
- Circular dependency resolution for object initialization in the global space
- Thread local objects
- Loops:
  - For iterator loop (*similar to for loops in the Rust programming language*)
  - While loop (*similar to for loops in the C and C++ programming languages*)
- Interfaces via Contract and impl (*similar to trait and impls in Rust*)
- Language defined generic unicode string interface that supports extensive unicode functionalities
- Robust compile time evaluation semantics
- Explicit and implicit default value argument entry
- Value argument list generators (*allows value list generation in any value argument entry*)
- Access restriction semantics (*controls the visibility of language items*)
- Import system
- Compile time polymorphism:
  - Type parameters (_parametric polymorphism in programming or colloquially known as generics_) that support generic typing
    - Type constructor type parameter (_similar in concept to Higher Kinded Types in Haskell but limited in semantics to keep it simple_)
  - Compile time value parameters (_basically the value parameter version of type parameters, can be seen in parametric polymorphism implementation in languages like Rust and C++_)
- Run time polymorphism:
  - Contract types (_basically impl types in Rust but with a significantly different implementation_)
- Groupings (_pinnacle of less typing and semantic syntax grouping in a high level context_)
- Variadics (_similar in concept to parameter packs in C++ which are just simply compile time type safe variadics_)
- Tuples and variants (_basically anonymous product and sum types enabled by the variadics feature_)
- Language communication interface (_**LCI**_):
  - Attribute LCI (_includes the various language constraints and many more_)
  - Expression LCI (_exposes interfaces to language metadata and special language functions_)
  - Type LCI (_exposes interfaces to language type system metadata_)
  - Miscellaneous LCI (_involves unrelated special language functionality_)
- Constraint application (_allows the entry of user defined constraint on various language high-level constructs_)
- Unified function call
- Redefined precedence for some operators
- Limited operator overloading
- Operator combinations (*allows for chaining certain operators*)
- Collection expressions
- Literal tags (*known as literal types in C++*)
- Custom collection expression definition
- Custom literal tag definition
- Blocks as expressions
- Conditional expressions:
  - If conditional expression
  - Match conditional expression
  - Or-field query conditional expression (_a more robust form of pattern matching expression in functional languages and Rust_)
- References:
  - Value references (_similar in concept to references in C++ and Rust_)
    - Non allocating value references
    - Allocating value references
  - Memory address references (_similar in concept to pointers in C and C++_):
    - Non allocating memory address references
    - Allocating memory address references
- Implicit lifetime semantics (_similar in concept to explicit lifetime parameters in Rust_)
- Scope definitions (_similar in concept to `namespaces` in C++_)
- Compile time type creator introspection
- Value unpacking (_similar to structured binding in C++ but way more expressive and robust_)
- 1-based indexing (*subjectively better than 0-based indexing for me*)
- Foreign interface
- White-space decisive parsing
- Well defined language semantics
- Excellent compiler error messages called error logs

## Prospective Features

- Concurrency aware programming
  - Thread types and constraint semantics for multi-threading
  - And others
- SIMD programming (*implemented natively in static arrays*)
- Implementation of the platform (*programming area*) aware computing feature
- Native assembly language entry with a generic assembly language
- Native integration with nc markup language or, preferably, a graphics language of some kind, which would emulate svelte's design in a way to redefine graphical user interface programming. To be used in both the web and systems platforms.

## Nc Programming Language Examples

Due to NPL not having syntax highlighting yet in the code section of markdown, the Rust programming language is selected as the programming language, to use its syntax highlighting because it is the only language included that remotely resembles NPL syntax. It is for this same reason that NPL discard and document single-line comment contents (`>!` & `>:`)  are enclosed with double quotes to prevent syntax highlighting, since the comments syntax are different than Rust's.

- Hello world example

```rust
import marco std:io:print

fn main {
    print("Hello World from NPL :)")
}
```

- Raw user string identifier and raw language identifier entry example

```rust
fn main {
    obj _ r"Do you love 🐻s?" = true
    obj _ r'for = "Damn! using the `for` language identifier as a user identifier"
    obj _ r"Are you an ape(🦍)?" = true
    obj _ r'struct = "Wow! using the `struct` language identifier as a user identifier"
}
```

- References example

```rust
import scope std:mem:allocator

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
    obj: allocator:basic[ui4].free(alloc)
}
fn alloc_memory_address_ref(obj alloc: {*}ui4) {
    obj: allocator:basic[ui4].free(alloc)
}
```

- Sum type creator example

```rust
import marco std:io:printf

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

- Value Unpacking example

```rust
import type std:string:string
import marco std:io:printf

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
    >! "Due to redefined precedence levels in NPL, the above expression evaluates as `((&bicycle).display)()`"
}

>! "Value unpacking can also be applied to and-fields(objects in struct) and normal objects too"
```

- Contract and impl with runtime polymorhism example

```rust
import marco std:io:printf

contract[type Self] animal =
fn sound(obj self: Self) &str;
fn name(obj self: Self) &str;
end

struct (dog, cat);

scope @dog =
impl[dog] animal =
fn sound(obj _: dog) &str {
    "woof"
}

fn name(obj _: dog) &str {
    "Dog"
}
end
end scope

scope @cat =
impl[cat] animal =
fn sound(obj _: cat) &str {
    "meow"
}

fn name(obj _: cat) &str {
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
import type std:string:string

marco add[type T](obj (lhs, rhs): T) T apply @T eq @string or eq @ui4 {
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

import marco std:io:printf

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

import type std:(ds:arrayList, misc:maybe)

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
import marco std:io:printf

fn main {
    obj static_array: arr[ui4]!(1024)
    
    >! "Delay initialization "
    static_array := arr[->> for x in 1~1024 {x + 3}]
    
    >! "Essentially results in `arr[1+3, 2+3, 3+3, ..., 1024+3]`"
}
```

- Matrix and vector implementation using static arrays and collection expressions example

```rust
import marco std:io:printf

fn main {
    >! "Matrix"
    obj _ = obj: matrix([[3.0, 4.0], [3.0, 4.0]]) >! "Using object constructors"
    obj _ = matrix[[3.0, 4.0], [3.0, 4.0]] >! "Using collection expressions"
    
    >! "Vector"
    obj _ = obj: vector([2.0, 3.0]) >! "Using object constructors (2d vectors)"
    obj _ = vector[2.0, 3.0] >! "Using collection expressions (2d vectors)"
    
    >! "Others"
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
use marco operator.[] 	>! "For (1-based)indexing"
use impl display 		>! "For printing values in a displayable format"

end scope
```

- Compile time type creator introspection example

```rust
import marco std:io:printf

fn main {
 
	obj person_struct = exp:getTypeCreatorMetadata[person, array]()

    printf("TypeCreator\t[$(person_struct.kind)]\nType\t\t[$(person_struct.typeName)]\n")
    
    person_struct => fieldInfoList {
        obj fieldInfoListIter = &fieldInfoList.iter()

        >! "Extract the first element out of the iterator"
        fieldInfoListIter.next() => some(fieldInfo) {
        	printf("AndFields\t[$(fieldInfo.name):$(fieldInfo.typeName)")
        }else {}
        
        for fieldInfo in fieldInfoListIter {
            printf(", $(fieldInfo.name):$(fieldInfo.typeName)")
        }
        printf("]\n")
    }else {}
    
    >! "Prints:" 
    >! "TypeCreator	[struct]"
    >! "Type		[person]"
    >! "AndFields	[name:&str, age:ui1, location:location]"
}

struct person = obj (name: &str, age: ui1, location: location)
struct location = obj (longitude, latitude): r4
```