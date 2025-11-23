# NcLang

Nc programming language or informally called ncLang is a next generation constraint based strongly typed programming language that aims to redefine the programming space by incorporating any and all current technologies in the programming space while also making it possible to easily integrate future technologies with its robust design.

It is a language that is designed from its infancy to accommodate every known area of programming and also, importantly, make the programmer's experience near equal or comparable to programming languages designed for those known areas. The language does this by centralizing specific functionalities of those areas of programming and allowing the programmer to only use them when programming for those areas. An example of said functionality would be using the programming language as a systems programming language, mobile systems programming language, **GUI** programming language, web programming language, scripting programming language and many more(Although it cannot be used as a data language, that is **JSON** or **XML**, nc data representation language already serves such purpose and is natively integrated in nc programming language).

It is essentially a platform aware language and it is for this reason the I call the language a **TGPL**(Truly General Purpose Programming Language).

## NcLang Features

- Positional base number entry from bases 2 to 36 (For both integer and real numbers)
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
- Highly expressive type system
- Stack array type(An array data structure that only uses the stack memory space invented just for the language)
- Static array type
- Integer range types
- Product type creators (Similar to structs in C and Rust)
- Sum type creators (Similar to enums in Rust and unions in C and C++)
- Semantic type creators (Similar to derived types in Ada but with added semantics)
- Semantic ranged integer type creators (Similar to Integers in Ada)
- Value definition type creators (Similar to enum classes in C++)
- Type constructors (Similar in concept to Higher Kinded Types in Haskell but limited in semantics to keep it simple)
- Value semantics:
  - Move value semantics (Non destructive move unlike in rust and like in C++)
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
- Language defined generic string interface
- Robust compile time evaluation semantics
- Explicit and implicit default value argument entry
- Value argument list generators (Allows value list generation in any value argument entry)
- Access restriction semantics (Controls the visibility of language items)
- Import system
- Compile time polymorphism:
  - Type parameters (Basically generics in some programming languages and parametric polymorphism in programming)
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
  - Memory address references (Similar in concept to pointers in C and C++):
    - Non allocating memory address references (Basically raw pointers in C and C++)
    - Allocating memory address references (Higher form of smart pointers in C++)
- Implicit lifetime semantics (Similar in concept to explicit lifetime parameters in rust)
- Scope definitions (Similar in concept to namespaces in C++)
- Run time type introspection
- Value unpacking (Similar to structured binding in C++ but way more expressive and robust)
- Foreign interface
- Platform agnostic computing
- Well defined language semantics
- Excellent compiler error messages called error logs

## NcLang Examples

- Hello world example

```rust
import marco std:print

fn main {
    print("Hello World(from nc programming language)\n")
}
```

- References example

```rust
import type std:alloc:basic

fn value_ref(obj _: &ui4) {}
fn memory_address_ref(obj _: *ui4) {}
fn alloc_memory_address_ref(obj alloc: {*}ui4) {
    obj: alloc:basic[ui4].deallocate()
}

fn main {
    obj a: ui4()
    
    value_ref(&a)
    memory_address_ref(addressof a)
    alloc_memory_address_ref(obj: alloc:basic[ui4].allocate())
}
```

- Contract and impl with runtime polymorhism example

```rust
import marco std:printf

contract[type Self] animal =
fn sound(obj self: &Self) &str
end

struct (dog, cat)

scope @dog =
impl[dog] animal =
fn sound(obj _: &Self) {
    -> "bark"
}
end
end scope

scope @cat =
impl[cat] animal =
fn sound(obj _: &Self) {
    -> "meow"
}
end
end scope

fn animal_sound(obj animal: !animal) {
    printf("Animal makes this sound: $(animal.sound())")
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

marco add[type T](obj (lhs, rhs): T) T apply @T eq string or ui4 {
    -> lhs + rhs
}

fn main {
    obj _ = add(34, 45)
    obj _ = add(string"Daniel", string" Emeka")
}
```

- Variadics for functions and constraint application example

```rust
fn sum(obj ..args: ui4) ui4 apply variadics(args).size gt 2 {
    obj result: ui4()
    
    for arg in variadics(args) {
        result += arg
    }
    -> result
}
```

- Type constructors example

```rust
>! Haskell functor: fmap :: f a -> (a -> b) -> f b

contract[type Self[?]] functor[type A] =
fn fmap[type (B, Fn)](obj (self: Self[A], fcn: Fn)) Self[B] apply @Fn impls fn(A)B
end

import type std:(arrayList, maybe)

>! ArrayList implementing functors
scope @arrayList[type T] =
impl[arrayList] functor[T] =
fn fmap[type (B, Fn)](obj (self: arrayList[T], fcn: Fn)) Self[B] apply @Fn impls fn(T)B {
    -> self.map(fcn)
}
end
end scope

>! maybe implementing functors
scope @maybe[type T] =
impl[maybe] functor[T] =
fn fmap[type (B, Fn)](obj (self: maybe[T], fcn: Fn)) Self[B] apply @Fn impls fn(T)B {
    -> self => some {
        obj: maybe(some)
    }else
}
end
end scope
```
