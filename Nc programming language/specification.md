# Nc Programming Language Official Specification

This document defines the formal specification of the nc programming language which would be used to write the compiler of the nc programming language, form tutorials for the nc programming language and be the source of reference to any questions, debates, academic talks or texts about the nc programming language. Nc programming language supports both **Just In Time** (***JIT***) and **Ahead Of Time** (***AOT***) compilation, **Just in Time** compilation would be used to implement its compile time features and by extension its not so conventional interpreter, all would be discussed at length in this document. Unlike most formal specifications, this document is written in a beginner friendly manner to facilitate faster understanding of the document for persons that have met the criteria of possessing rudimentary knowledge in programming concepts, the nc text processing language and compiler development.

## Author

The author of this specification document is the creator of the nc project **Daniel Emeka**. In subsequent sections, in matters that requires self referencing, the author will refer to himself in the first person primarily to create an informal tone in the midst of this formal document. It is a contrast the author wishes to convey in this document.

---

It is encouraged to read this specification document as a markdown document using a dedicated markdown editor or viewer like **Typora** because of it's continuous flow, meaning unlike the PDF version, it isn't divided into pages.

An example of the Typora interface:

![TyporaExample](TyporaExample.png)

The official acronym of the programming language is **NPL** which stands for **N**c **P**rogramming **L**anguage - obviously - and the official source code file extension is `.npl`.

To describe the text representation of the nc programming language, nc's very own text processing language is used which is **nc text processing language** and would be referred to using its acronym or informal name **NTPL** in this document. You are advised to read the tutorial for the text processing language before reading this document.

> I also currently use `json` as the language of choice for the NTPL code sections because NTPL does not yet have syntax highlighting.

---

NPL is comprised of four basic parts, like all programming languages, which are:

1. Comments
2. Tokens
3. High-level construct syntax
4. High-level construct semantics

Comments are informal constructs ignored by the programming language used to convey expression of thought, intent or ideas in code, tokens are the fundamental units of the programming language, high-level construct syntax describes the format of the various high-level constructs built from tokens and high-level construct semantics details the meaning of the various high-level construct syntax, where they are expected to be, their use and their low-level implementations in an abstract manner.

To implement greater understanding of this document and to keep with the promise of it being written in a beginner friendly way, the four basic parts would be explained explicitly one after the other while also enumerating their co-dependence.

## Comments

Like was previously said, comments are informal constructs ignored by the language used to convey expression of thought, intent or ideas in code. They are referred to as informal because they are not a formal feature of the language that has any impact on the compilation of code because they are ignored by the language after a certain phase of compilation. Their main purpose it to convey your expression of thought to yourself in the future and other programmers going over your code, convey your intent over a particular section of code to others and convey ideas used in the planning of the writing of code.

Comments are generally categorized into two in programming, that is:

- Single-line comments
- Multi-line comments

With their names already been self descriptive, single-line comments are comments that span a single-line while multi-line comments are comments that span multiple lines.

There are two types of comments in NPL, namely:

- Discard comments
- Document comments

### Discard Comments

Are comments that are simply discarded by the compiler after the fact (_generally after the tokenization phase of the compiler or a special comment parsing phase before tokenization_). 

Based on the categories of comments, there are two type of discard comments, namely:

- Single-line discard comments
- Multi-line discard comments

#### Single-Line Discard Comments

Below is the single-line discard comments syntax written in NTPL:

```json
singleLineDiscardComment = '>! ' any*
```

Examples of the above syntax would be:

```
>! Writing a signle-line comment
>! obj x = 34
>! 
```

#### Multi-Line Discard Comments

Below is the multi-line discard comments syntax written in NTPL:

```json
multiLineDiscardComment = '<\'' any* '\'>'
```

An example of the above syntax would be:

```
<'
	comment
	spanning
	muliple
	lines
'>
```

### Document Comments

Are comments that are retained by the compiler after the fact (_generally after the tokenization phase of the compiler or a special comment parsing phase before tokenization_). Reason being that document comments serve the purpose of writing documentations or meaningful text that help describe the intent of code. Therefore, all document comments are retained by the compiler to be used in generating documentations of code when prompted by the user, further explanation would be given in the semantic section.

Based on the categories of comments, there are two types of document comments, namely:

- Single-line document comments
- Multi-line document comments

#### Single-Line Document Comments

Below is the single-line document comment syntax written in NTPL:

```json
singleLineDocumentComment = '>: ' any*
```

Examples of the above syntax would be:

```
>: This code performs heterogeneous independent computations simultaneously
>: Only god knows what this code means, sorry 😭
```

#### Multi-Line Document Comments

Below is the multi-line document comments syntax written in NTPL:

```json
multiLineDocumentComment = '<"' any* '">'
```

An example of the above syntax would be:

```
<"
	Given the inception of SIMD intrisntics, this code is due to change to use the new
	technology that promises more speed when operating on large datasets such as this,
	but due to my chronic laziness, I would not be able to implement such change until
	the end of the year. Besides, I don't get paid for any of this, so do not flood my
	emails or telegram with texts of the implementation :).
">
```

## Tokens

Like was previously said, tokens are the fundamental units in the nc programming language, they comprise of a set of unicode characters that have a predefined purpose in the nc programming language.

There are 3 types of tokens, namely:

1. Identifier tokens
2. Literal tokens
3. Symbol tokens

### Identifier Tokens

Are tokens that make use of a set of unicode characters that can be combined to form text that depends on a *speaking* language and the context it is written in. Below is the basic identifier syntax written in NTPL:

```json
basicIdentifierToken = '_'|Script ('_'|Script|'0'~'9')*
```

Examples of the above syntax would be:

```
i_love_myself
我爱我自己
私は自分自身を愛している
Я_люблю_себя
Kendimi_seviyorum
Me_quiero
أنا_أحب_نفسي
__delta__
_123456
km1
km_8
```

There are two types of Identifier tokens, namely:

1. Language identifier tokens
2. User identifier tokens

#### Language Identifier Tokens

Are the set combination of unicode characters that are reserved for use by the language. Below are the language identifier tokens:

- `scope`
- `contract`
- `impl`
- `struct`
- `union`
- `valueDef`
- `unique`
- `obj`
- `type`
- `fn`
- `marco`
- `break`
- `continue`
- `true`
- `false`
- `addressof`
- `and`
- `or`
- `not`
- `xor`
- `mut`
- `from`
- `eq`
- `lt`
- `gt`
- `if`
- `else`
- `while`
- `for`
- `match`
- `with`
- `in`
- `import`
- `apply`
- `r`
- `use`
- `_`
- `outer`
- `end`
- `variadic`
- `at`
- `exp`
- `ty`
- `misc`
- `operator`

---

Obviously the NTPL function for language identifier tokens is `languageIdentifierToken` equal to the language identifier tokens list above, but since they are too much, I am not going to write the NTPL it, just imply it.

#### User Identifier Tokens

Are the rest of the set combination of unicode characters that the user can make use of.

##### Raw User Identifier Tokens

To eliminate the restriction that only allows the use of a small set of unicode characters to be used in writing identifiers and also the restriction of reserving a set combination of identifiers for the language, NPL has something called raw user identifier tokens.

There are two types of raw user identifier tokens, namely:

- Raw user language identifier tokens
- Raw user string identifier tokens

###### Raw User Language Identifier Tokens

Are raw user identifier tokens that allow the entry of language identifiers as user identifiers. Below is the syntax written in NTPL:

```json
rawLanguageIdentifierToken = 'r\''languageIdentifierToken
```

Examples of the above syntax would be:

```
r'struct
r'union
r'scope
```

###### Raw User String Identifier Tokens

Are raw user identifier tokens that allow the entry of any unicode character to form an identifier, provided it does not form into a basic identifier token. Below is the syntax written in NTPL:

```json
rawUserIdentifierToken = 'r'stringTextLiteralToken
```

> stringTextLiteralToken is covered in the string text literal token section under the literal token section

Examples of the above syntax would be:

```
r"Happy Birthday 🎂"
r"🦍"
r"is car flying?"
```

As earlier stated, a raw user identifier token must not form into a basic identifier. This is done because raw user string identifiers were introduced solely to supplement user identifier entry, and since there already exist basic identifiers, having another identifier type form into a basic identifier just leads to confusion. Therefore something like the below is not allowed:

```
r"come_and_go_by_yeat"
r"Travis_Scott"
r"isThisTrue"
```

Besides, anything else goes in a raw user string identifier token entry, a user can start identifiers with numbers `r"1Egg"`, include whitespace unicode characters `r"1 Egg"`  and have fun with emojis `r"🕵 is 👁 at 🫵🏿"`. The sky is literally your limit with raw user string identifier tokens.

---

Subsequently, the NTPL function for identifier tokens is:

```json
identifierToken = languageIdentifierToken|userIdentifierToken
```

With `userIdentifierToken` encompassing the remaining set combination of unicode characters and raw user identifier tokens.

### Literal Tokens

Are tokens that make use of a set of unicode characters that can be combined to form semantic constant values.

There are two types of literal tokens, namely:

- Number literal tokens
- Text literal tokens

#### Number literal tokens

Are tokens that allow the entry of numbers in NPL. Number literal tokens in NPL are positional numeral system numbers that support bases `2` to `36` and digit separators(`_`). Due to the fact that number literal tokens in NPL support bases `2` to `36`, unicode characters `A` to `Z` are valid digits. Detailed explanation of positional numeral system can be found in [**TODO: create a document to explain positional numeral systems**]. Below is the digits and base entry syntax written in NTPL:

```json
digits = '0'~'9'|'A'~'Z'

base = ₂~₃₆
```

The default base of a number literal when no base is specified is base `10`.

There are two types of number literal tokens, namely:

- Integer number literal tokens
- Real number literal tokens

##### Integer Number Literal Tokens

Are number literal tokens that allow the entry of whole numbers (_all digits including zero_). Below is the syntax written in NTPL:

```json
integerNumberLiteralToken = '0'~'9' ('_'? digits)* base?
```

Examples of the above format would be:

```
10_000
3J5L₂₂
0FF_90₁₆
0DDN₂₅
10_000₁₉
```

Because of the need to disambiguate between identifiers and numbers, digits `0` to `9` are expected as the first digit in an integer number literal token entry, so writing the hexadecimal number `AB4₁₆` would be `0AB4₁₆`.

##### Real Number Literal Tokens

Are number literal tokens that allow the entry of rational numbers (_fractional numbers, numbers that are represented as a ratio of two integers_) and irrational numbers (_non fractional numbers - numbers that cannot be represented as a ratio of two integers_).

Real number literal tokens can either be written in either normal fractional number form `0.0003` or scientific notation form `3.0@-4` or `3@-4`. Because number literal tokens in NPL support bases `2` to `36`, the exponent base indicator is  `@` unicode character not the conventional `e` or `E` with the exponent base being the number after the exponent base indicator. Since the exponent base refers to the count of digits to move the fractional point by, the language only parses for base 10 digits as the exponent base which is then used to refer to the exact number of digits to move the fractional point by. Below is the real number literal token and exponent syntax written in NTPL:

```json
realNumberLiteralToken = '0'~'9' ('_'? digit)* '.' digit ('_'? digit)* base? exponent?

exponent = '@' '-'? '0'~'9'+
```

Examples of the above format would be:

```
23.34
2.345@-90
0.34₈
2G.KL₂₈@2
```

#### Text Literals Tokens

Are literal tokens that allow the entry of any unicode character and something called a text action in them.

#### Text Actions

Are a set combination of unicode characters starting with `\` unicode character that instructs the language to perform a particular action in the text literal token. Below are the syntax list of the various text actions written as NTPL expressions:

- `r'\n'` : inserts the newline unicode character

- `r'\t'` : inserts the horizontal tab unicode character

- `r'\e'` : inserts the escape unicode character

- `r'\r'` : inserts the carriage return unicode character

- `r'\"'` : inserts the apostrophe unicode character

- `r'\\'` : inserts the `\` unicode character

- `r'\'WhiteSpace+` : discards any whitespace character till a non whitespace character is found

- `r'\'unicode_character_codepoint` : allows the entry of unicode characters using their code-points

  - ```json
    unicode_character_codepoint = '['integerNumberLiteralToken']'
    ```

    Example of the above format would be `\[345]`

    > **NOTE**: when no base is specified for the integer number literal token, instead of defaulting to base 10 like the default for number literal tokens, the language defaults to base 16, this is to better reflect the prominent base used in specifying code-points in unicode

- `r'\'unicode_character_name` : allows the entry of unicode characters using their names

  - ```json
    unicode_character_name = '{'basicIdentifierToken (' '|'-' basicIdentifierToken)*'}'
    ```
    
    Example of the above format would be `\{face with crossed-out eyes}` which is the 😵 unicode character.

Subsequently, the NTPL function of text action is `text_action` equal to the various text actions above.

---

There are two types of text literal tokens, namely:

- Character text literal token
- String text literal token

##### Character Text Literal Tokens

Are text literal tokens that allow the entry of exactly one unicode character or text action that results in a unicode character. Below is the syntax written in NTPL:

```json
characterTextLiteralToken = '\'' any|text_action '\''
```

Examples of the above format would be:

```
'\n'
'e'
'ざ'
'🌉'
'Ǽ'
'\                      E'
'엓'
```

Character text literal token allows the entry of the `'` character by just specifying three `'` characters like so `'''` and the entry of `\` without the text action by just specifying one `\` like so `'\'`, these are all possible due to the fact that character text literal tokens expect only one unicode character.

##### String Text Literal Tokens

Are text literal tokens that allow the entry of zero or more unicode characters. There are two types of string text literal tokens, namely:

- Formatted string text literal tokens
- Unformatted string text literal tokens

###### Formatted String Text Literal Tokens

Are string text literal tokens that support the entry of text actions. Below is the syntax written in NTPL:

```json
formattedStringTextLiteralToken = '"' (any|text_action)* '"'
```

Examples of the above format would be:

```
"\r\n"
"
I love me\
some good 🐔
"
"scarf(🧣) or sari(🥻)?"
""
"\n㒐㦀\n"
```

###### Unformatted String Text Literal Tokens

Are string text literal tokens that do not support the entry of text actions, meaning text actions simply have no effect in the string text literal token. Below is the syntax written in NTPL:

```json
unFormattedStringTextLiteralToken = '#'{n} '"' any* '"' '#'{n}
```

> Remember, the curly brace operator in the above NTPL asks for at least one or exactly **n** iterations of the unicode character **#**, meaning the number of both **#** must be the same

Examples of the above format would be:

```
#"Collectivism is the enemy of Individualism"#
##" "# "# "##
#"\n\\r\r\r\r\r\r\r\r\rn"#
```

---

Subsequently, the NTPL function of string text literal token is:

```json
stringTextLiteralToken = formattedStringTextLiteralToken|unformattedStringTextLiteralToken
```

#### Literal Token Tags

Are simply marker identifiers that specify the type of literal tokens in NPL (_more in the semantic section_). Below is the number literal token and text literal token syntax with their literal token tag specifications written in NTPL:

```json
numberLiteralToken = integerNumberLiteralToken|realNumberLiteralToken '\'' identifierToken

textLiteralToken = identifierToken characterTextLiteralToken|stringTextLiteralToken
```

#### Symbol Tokens

Are the remaining set of unicode characters that are used in the language. They are called symbols because the language uses them as such and unlike identifier and literal tokens, individual symbol tokens are fixed and not extendable. Below are the unicode characters that form the list of symbol tokens:

- `+`
- `-`
- `%`
- `*`
- `/`
- `^`
- `=`
- `:=`
- `+=`
- `-=`
- `=-`
- `*=`
- `/=`
- `=/`
- `%=`
- `=%`
- `^=`
- `!`
- `~`
- `~.`
- `:`
- `(`
- `)`
- `{`
- `}`
- `[`
- `]`
- `&`
- `#`
- `@`
- `$`
- `=>`
- `->`
- `~>`
- `->>`
- `,`
- `.`
- `;`
- `..`
- `?`
- `.[`
- `.{`

---

Obviously the NTPL function for symbol tokens is `symbolToken` equal to the symbol tokens list above, but since they are too much, I am not going to write it, just imply it.

## High-Level Construct Syntax

Like was previously said, high-level construct syntax describes the format of the various high-level constructs built from tokens. The following are the various high-level construct syntax in NPL:

- File content syntax
- Type syntax
- Objects syntax
- Parameters entry syntax
- Arguments entry syntax
- Constraint application syntax
- Function syntax
- Marco syntax
- Type creators syntax
- Contract syntax
- Impl syntax
- Scope syntax
- Expressions syntax
- Block syntax
- Statement syntax
- LCIs (_Language Communication Interfaces_) syntax
- Import syntax
- Use syntax
- Groupings syntax



Needed NTPL function in this section:

```json
list($exp:exp, $separator:exp = ',', $op:op = `*`) = $exp ($separator $exp)`$op`
```

### Format for this section

Unlike the comment and token sections, this section has a fixed format for how the information of the various syntaxes would be presented. First would be the primary syntax of the high-level construct in NTPL, second would be the secondary-syntax of the high-level construct in NTPL, if any, third would be the auxiliary syntax in NTPL, if any, that would be used to display additional helper syntaxes directly linked to the high-level construct, fourth and finally would be supplementary info, if any, that includes additional essential information that cannot be represented in NTPL or is better represented in textual format on the parsing of the high-level construct syntax.

The format of this section shown in NTPL for fun:

```json
highLevelConstructSyntaxSection = primarySyntax secondarySyntax? auxiliarySyntax? supplementaryInfo?
```

 Obviously, the above NTPL function has no real purpose in this NPL specification other than to describe the format of this section.

The reason for the distinction between primary and secondary syntaxes is that there are some syntaxes that do not exactly belong in the primary syntax label and also do not belong at all in the auxiliary syntax label, so, a separate syntax label is made for them.

### File Content Syntax

Simply refers to the various high-level construct syntaxes that are allowed in the high-level construct syntax level to be written in an NPL code file. They are also referred to as standalone high-level constructs because they can be written independently in an NPL code file.  Below is the NTPL for it:

```json
fileContent = (object|function|marco|scope|import|contract|typeCreator)*
```

### Type Syntax

Below is the type syntax written in NTPL:

```json
type = basicType|functionType|contractType|valueReference|memoryAddressReferenceType|typeLCI|typeFromExpression
```

Auxiliary syntaxes for types syntax written in NTPL:

```json
basicType = scopedIdentifier typeArgumentEntry? comptimeValueArgumentEntry?

functionType = 'fn' '('list(type)')' type|'!'

contractType = '!' ('mut'? '&')? functionType|(userIdentifierToken typeArgumentEntry?)

valueReferenceType = 'mut'? '&'|'{&}' type

memoryAddressReferenceType = 'mut'? '*'|'{*}' type

typeFromExpression = '[' expression ']'
```

### Objects Syntax

Below are the objects syntax written in NTPL:

```json
objects = object|valueParameter|field|functionExpressionValueParameter
```

Secondary syntaxes for objects syntax written in NTPL:

```json
object = 'obj' mainObjectPart|objectGrouping

valueParameter = 'obj' basicValueParameter|variadicValueParameter|valueParameterGrouping

field = 'obj' basicField|variadicField|fieldGrouping

functionExpressionValueParameter = 'obj' functionExpressionValueParameterPart|functionExpressionValueParameterGrouping
```

Auxiliary syntaxes for objects syntax written in NTPL:

```json
directInit = valueArgumentEntry

indirectInit = '=' expression

objectTypeEntry = ':' type (directInit|indirectInit)?

objectIdentifier = ('_'|('mut'? userIdentifierToken))|('_' userIdentifierToken)

unpackingEntry = '[' list(userIdentifierToken|'_'|'.'|unpackingEntry) ']'

mainObjectPart = objectIdentifier|('mut'? unpackingEntry) (objectTypeEntry|indirectInit)?

basicValueParameter = objectIdentifier|('mut'? unpackingEntry) ':' type indirectInit?

variadicValueParameterPart = ('..' 'mut'? userIdentifierToken)|('_' '..' userIdentifierToken)

variadicValueParameter = variadicValueParameterPart ':' '..'? type

basicField = 'mut'? userIdentifierToken|unpackingEntry ':' type

variadicField = '..' 'mut'? userIdentifierToken ':' '..'? type

functionExpressionValueParameterPart = objectIdentifier|unpackingEntry (':' type)?
```

### Parameters Entry Syntax

Below are the parameters entry syntax written in NTPL:

```json
valueParameterEntry = '('list((attributeLCI? valueParameter))')'

comptimeValueParameterEntry = '!'.'('list((attributeLCI? valueParameter))')'

functionExpressionValueParameterEntry = '('list(functionExpressionValueParameter)')'

typeParameterEntry = '['list(typeParameter)']'
```

Sub syntaxes for parameters entry syntax written in NTPL:

```json
typeParameter = basicTypeParameter|variadicTypeParameter
```

Auxiliary syntaxes for parameters entry syntax written in NTPL:

```json
basicTypeParameter = 'type' userIdentifierToken typeArgumentEntry?

variadicTypeParameter = 'type' '..' userIdentifierToken
```

### Arguments Entry Syntax

Below are the arguments entry syntax written in NTPL:

```json
valueArgumentEntry = '('list(valueArgument)')'

comptimeValueArgumentEntry = '!'.'('list(valueArgument)')'

typeArgumentEntry = '['list(typeArgument)']'

attributeLCIArgumentEntry = '('attributeLCIArgumentEntryPart1|attributeLCIArgumentEntryPart2')'
```

Auxiliary syntaxes for arguments entry syntax: written in NTPL

```json
valueArgument = expression|parameterValueArgument|valueArgumentListGenerator|expressionCodeArgument|'_'

parameterValueArgument = '.'userIdentifierToken '=' expression|'_'

valueArgumentListGenerator = '->>' customLoopStatement

customLoopStatement = loopStatementHead primaryExpression

loopStatementHead = forLoopStatementHead|whileLoopStatementHead

forLoopStatementHead = 'for' (list(object) ';')? userIdentifierToken 'in' expression

whileLoopStatementHead = 'while' (list(object) ';')? expression (';' expression)?

expressionCodeArgument = '~>' expression

typeArgument = typeArgumentFieldIdentifierAssociation|parameterTypeArgument|'_'

parameterTypeArgument = '.'userIdentifierToken '=' attributeLCI? typeArgumentFieldIdentifierAssociation|'_'

typeArgumentFieldIdentifierAssociation = (type ('/'userIdentifierToken)?)|('/'userIdentifierToken)

attributeLCIArgumentEntryPart1 = userIdentifierToken'$'

attributeLCIArgumentEntryPart2 = ('scope' 'in')? 'mod'|'pkg'
```

### Constraint Application Syntax

Below is the constraint application syntax written in NTPL:

```json
constraintApplication = 'apply' logicalBinaryExpression|'_'
```

### Function Syntax

Below is the function syntax written in NTPL:

```json
function = 'fn' captureSpace? functionIdentifier valueParameterEntry? returnEntry? constraintApplication? block|';'
```

Auxiliary syntaxes for function syntax written in NTPL:

```json
caputreSpace = '|'list(expression|(userIdentifierToken '=' expressions))'|'

returnEntry = type|'type'|'!'

functionIdentifier = userIdentifierToken|grouping(userIdentifierToken) typeParameterEntry? comptimeValueParameterEntry?
```

### Marco Syntax

Below is the marco syntax written in NTPL:

```json
marco = 'marco' marcoIdentifier valueParameterEntry? returnEntry? constraintApplication? block|';'
```

Auxiliary syntaxes for marco syntax written in NTPL:

```json
marcoIdentifier = userIdentifierToken|miscLCI|operator|grouping(userIdentifierToken|miscLCI|operator) typeParameterEntry? comptimeValueParameterEntry?

operator = 'operator' operator

operator = [todo]
```

### Type Creators Syntax

Below are the type-creators syntax written in NTPL:

```json
typeCreators = structTypeCreator|unionTypeCreator|valueDefCreator|uniqueTypeCreator
```

Secondary syntaxes for type creators syntax written in NTPL:

```json
structTypeCreator = 'struct' genericTypeCreatorIdentifier constraintApplication? ('=' list(field))|';'

blankStructTypeCreator = 'struct' '=' list(field)

unionTypeCreator = 'union' genericTypeCreatorIdentifier constraintApplication? ('=' list(field))|';'

valueDefTypeCreator = 'valueDef' typeArgumentEntry? userIdentifierToken|grouping(userIdentifierToken) '=' list(userIdentifierToken)

uniqueTypeCreator = 'unique' genericTypeCreatorIdentifier constraintApplication? '=' type uniqueTypeCreatorRangeEntry?
```

Auxiliary syntaxes for type creators syntax written in NTPL:

```json
genericTypeCreatorIdentifier = userIdentifierToken|grouping(userIdentifierToken) typeParameterEntry? comptimeValueParameterEntry?

uniqueTypeCreatorRangeEntry = 'from' integerNumberLiteralToken'~'integerNumberLiteralToken
```

### Contract Syntax

Below is the contract syntax written in NTPL:

```json
contract = 'contract' typeParameterEntry contractIdentifier contractInheritancePart? constraintApplication? contractBody
```

Auxiliary syntaxes for contract syntax written in NTPL:

```json
contractBody = '=' (contractContentPart|import)+ 'end'

contractIdentifier = userIdentifierToken|grouping(userIdentifierToken) typeParameterEntry?

contractContentPart = attributeLCI? function|marco|blankStructTypeCreator

contractInheritancePart = ':' list(userIdentifierToken, '+')
```

### Impl Syntax

Below is the impl syntax written in NTPL:

```json
impl = 'impl' typeArgumentEntry? implIdentifier constraintApplication? implBody|';'
```

Auxiliary syntaxes for impl syntax written in NTPL:

```json
implIdentifier = userIdentifierToken|grouping(userIdentifierToken) typeArgumentEntry?

implContentPart = attributeLCI? function|marco

implBody = '=' (implContentPart|import)+ 'end'
```

### Scope Syntax

Below is the scope syntax written in NTPL:

```json
scope = 'scope' scopeIdentifier constraintApplication? scopeBody
```

Auxiliary syntaxes for scope syntax  written in NTPL:

```json
scopeBody = '=' (scopeContentPart|impl|use|import)* 'end scope'

scopeIdentifier = (userIdentifierToken|typeScopeIdentifier)|grouping(userIdentifierToken|typeScopeIdentifier)

scopeContentPart = attributeLCI? function|marco|typeCreators|object|scope

typeScopeIdentifier = '@' userIdentifierToken typeParameterEntry? comptimeValueParameterEntry?
```

### Expressions Syntax

Below are the expressions syntax written in NTPL:

```json
expression = attributeLCI? assignmentBinaryExpression
```

Secondary syntaxes for expressions syntax written in NTPL:

```json
assignmentBinaryExpression = list(logicalBinaryExpression, assignmentBinaryOperator)

logicalBinaryExpression = list(equalityBinaryExpression, logicalBinaryOperator)

equalityBinaryExpression = list(relationalBinaryExpression, equalityBinaryOperator)

relationalBinaryExpression = list(rangeBinaryExpression, relationalBinaryOperator)

rangeBinaryExpression = list(additiveBinaryExpression, '~'|'~.')

additiveBinaryExpression = list(multiplicativeBinaryExpression, '+'|'-')

multiplicativeBinaryExpression = list(exponentiationBinaryExpression, '*'|'/'|'%')

exponentiationBinaryExpression = list(fromBinaryExpression, '^')

fromBinaryExpression = ('exp' 'from' scopedIdentifier typeArgumentEntry? comptimeValueArgumentEntry?)|('fn' 'from' dotBinaryExpression)|dotBinaryExpression

dotBinaryExpression = unaryPrefixExpression unaryPostfixOperator* ('.' scopedIdentifier|scopedIdentiferPart unaryPostfixOperator*)*

unaryPrefixExpression = (unaryPrefixOperator unaryPrefixExpression)|primaryExpression

primaryExpression = collectionExpression|(':'? scopedIdentifier)|'variadic'|expressionType|conditionalExpression|objectExpression|functionExpression|block|literal|precedenceEntry|grouping(expression|'_')|expressionLCI
```

Auxiliary syntaxes for expressions syntax written in NTPL:

```json
assignmentBinaryOperator = '='|':='|'+='|'-='|'*='|'/='|'%='|'^='|'=-'|'=/'|'=%'

logicalBinaryOperator = 'not'? 'and'|'or'|'xor'

equalityBinaryOperator = 'not'? 'eq'|'in'

relationalBinaryOperator = 'lt'|'gt' relationalBinaryOperatorCombinations?

relationalBinaryOperatorCombinations = 'and'|'or' equalityBinaryOperator|'lt'|'gt'

unaryPostfixOperator = functionCall|orFieldQueryConditionalExpression|('.['expression']')|('.{'expression'}')

functionCall = (typeArgumentEntry comptimeValueArgumentEntry? valueArgumentEntry)|(comptimeValueArgumentEntry valueArgumentEntry)|valueArgumentEntry

unaryPrefixOperator = '-'|'not'|('mut'? '&'|'addressof')

collectionExpression = userIdentifierToken? '['list(expression)']'
                                 
precedenceEntry = '('expression')'

expressionType = '@'.type

scopedIdentifier = (userIdentifierToken|'outer').scopedIdentifierPart?

scopedIdentifierPart = ':'.(userIdentifierToken|'outer'|grouping(scopedIdentifier)).(':'.(userIdentifierToken|'outer'|grouping(scopedIdentifier)))*

objectExpression = 'obj:' (type.valueArgumentEntry?)|grouping((type.valueArgumentEntry?))

functionExpression = 'fn' captureSpace? functionExpressionValueParameterEntry type? block

conditionalExpression = ifConditionalExpression|matchConditionalExpression

ifConditionalExpression = 'if' (list(object) ';')? list((expression block), '|')) elseBranch?

matchConditionalExpression = 'match' (list(object) ';')? expression 'with' list((expression block), '|') elseBranch?

orFieldQueryConditionalExpression = '=>' list(orFieldQueryBranch, '|') elseBranch?

orFieldQueryBranch = mainOrFieldQueryBranch|('{'userIdetifierToken'}')|('('userIdentifierToken')')

mainOrFieldQueryBranch = mainOrFieldQueryPart1 mainOrFieldQueryPart2? block

mainOrFieldQueryPart1 = userIdentifierToken|('{' list(userIdentifierToken, _, `+`) '}')

mainOrFieldQueryPart2 = ('('userIdentifierToken')')|('['list(userIdentifierToken)']')

elseBranch = 'else' block?
```

#### Supplementary Info

##### Precedence

Precedence defines the order of which operators evaluate their operands first, by making operators with higher precedence evaluate their operands before operators with lower precedence (_From here on out they would be referred to as precedence levels_). The layout of the primary expressions syntax is setup such as to identify the various NPL precedence levels from basic NTPL expressions with the sole ambiguity being `dotBinaryExpression` which would be clarified in this section. It works by simply making a precedence level into an NTPL function and having the lower precedence level NTPL function call the higher precedence level NTPL function, for example, an `additiveBinaryExpression` has a lower precedence than a  `multiplicativeBinaryExpression` because the LHS and RHS operand call in an `additiveBinaryExpresion` asks for the `multiplicativeBinaryExpression`,  which would be fully syntactically evaluated first, that is collected into an expression, before the additive operators are paired with the LHS and RHS `multiplicativeBinaryExpression` operands, that means an expression like so `2 + 5 * 4 - 3 / 6` equals this `2 + (5 * 4) - (4 / 6)`. Implementation can then easily be done in code by making each individual NTPL function in primary expressions syntax into a function, procedure, routine, method or whatever name your language of choice calls runnable blocks of code with possible parameter entry and return types.

The reason as to why it is setup this way was born out of convenience and that convenience later served an essential purpose. So, basically, it is convenient to represent and parse for precedence levels in the high-level construct syntax phase because it is optimal to parse for the expressions while also arranging them into precedence levels instead of parsing only for dumb expressions (_expressions without the arrangement of precedence_) in the high-level construct syntax phase then deferring precedence arrangement to the high-level construct semantic phase. This is only made possible because precedence level parsing has no compiler error consequence, meaning that it does not result in a compiler error, it is does, however, result in a logical error consequence, that is logical errors in code due to mismatches in precedence levels. As for the essential purpose it later grew to serve, the layout of the precedence levels into separate NTPL functions creates an opportunity to ask for certain precedence levels while leaving out some, an example of this is in the constraint application syntax, where a `logicalBinaryExpression` is asked for, thereby hindering the open parsing of the `assignmentBinaryExpression` (_reason for using the `logicalBainryExpression` in the constraint application syntax to ask for expressions is because the syntaxes, like struct, union, contract, impl and so on, that make use of the constraint application syntax ask for `=` after the expression of the constraint application, so to prevent parsing conflict, `assignmentBinaryExpression` is not asked for openly, rather its immediate higher precedence level is asked for instead, so entry of an `assignmentBinaryExpression` must be done with the `precedenceEntry` which encloses the `assignmentBinaryExpression` thereby preventing parsing conflict_).

###### The Ambiguity of `dotBinaryExpression`

`dorBinaryExpression` has a certain ambiguity to it, here is the syntax:

```json
unaryPrefixExpression unaryPostfixOperator* ('.' scopedIdentifier|scopedIdentiferPart unaryPostfixOperator*)*
```

The ambiguity lies in the precedence level of the dot operator and the `unaryPostfixOperator`. It is an ambiguity because merely looking at the syntax is not enough to accurately decipher the precedence levels of the two operators. Below is the explanation to eliminate the ambiguity:

```json
unaryPrefixExpression unaryPostfixOperator*
```

The above unequivocally parses for the `unaryPrefixExpression` first which has the higher precedence level, then parses for the `unaryPostfixOperator` which has a lower precedence level than the postfix expression.

```json
('.' scopedIdentifier|scopedIdentiferPart unaryPostfixOperator*)*
```

The above parses for the dot operator then scoped Identifier related syntax and finally parses for `unaryPostfixOperator`, the programming language gives the dot operator a higher precedence level than the postfix operator, so, the dot operator and its RHS operands (_`scopedIdentifier|scopedIdentifierPart`_) must be syntactically evaluated first before the `unaryPostfixOperator`. 

So, a syntactic evaluation of this `a.b()` would result in this `(a.b)()`, not this `a.(b())`, thereby keeping with the sane and intuitive programming precedence convention in programming languages that make use of the OOP method (_member function_) call style.

###### Precedence List

The below table shows the precedence levels of the various operators in NPL with the operators written as NTPL expressions, just to compliment what is already clearly stated using NTPL in the primary expressions syntax.

| Rank | Operator                                                     |
| ---- | ------------------------------------------------------------ |
| 12th | Binary assignment operators `'='`, `':='` , `'+='`, `'-='`, `'*='`, `'/='`, `'%='`, `'^='`, `'=-'`, `'=/'`, `'=%'` |
| 11th | Binary logical operators `'and'`, `'or'`, `'xor'`            |
| 10th | Binary equality operators `'eq'`, `'in'`                     |
| 9th  | Binary relational operators `'lt'`, `'gt'`                   |
| 8th  | Binary range operators `'~'`, `'~.'`                         |
| 7th  | Binary additive operators `'+'`, `'-'`                       |
| 6th  | Binary multiplicative operators `'*'`, `'/'`, `'%'`          |
| 5th  | Binary exponentiation operator `'^'`                         |
| 4th  | Binary from operator `'from'`                                |
| 3rd  | Unary postfix operators `functionCall`, `'.['expression']'`, `orFieldQueryConditionalExpression` |
| 2nd  | Binary dot operator `.`                                      |
| 1st  | Unary prefix operators `'-'`, `'not'`, `'mut'? '&'|'addressof'` |

There is also the notable mention of primary expressions from the NTPL of primary expressions syntax, which stay at a level unconstrained by precedence levels.

###### Precedence Deviation

Note that NPL does not exactly follow the precedence levels in conventional programming and mathematics, the following are the precedence deviations in NPL:

1. Binary logical operators precedence deviation

   In conventional programming and mathematics, there are defined precedence levels for the ***and***, ***or*** and ***xor*** binary logical operators which are stated in the table below:

   | Rank | Operator |
   | ---- | -------- |
   | 3rd  | `or`     |
   | 2nd  | `xor`    |
   | 1st  | `and`    |

   But in NPL, they all have the same precedence levels, this is done for two reasons, one, to shorten the amount of precedence levels a programmer has to learn and worry about and two, I see them as unintuitive primarily because I always encountered logical errors when using them without precedence entry, so I removed them to force the use of precedence entry whenever they are to be dealt with instead of relying on their precedence that may come back to bite you in the form of logical errors.

2. Unary prefix operators precedence deviation

   In conventional programming, the defined precedence level for all unary operators is always lower than the binary dot operator (_member operator in some languages_), but in NPL, the unary prefix operator has a higher precedence level than the binary dot operator, this is done for semantic ergonomics in the programming language that trades-off one convenience for another. In C or C++, for example, the use of this `&(a.b)` expression is more prevalent than the use of this `(&a).b` expression in the programming language (_in fact, it is not even a semantically valid expression in the programming language_), so, the set precedence level in the programming language allows for the entry of the more prevalent expression without precedence entry like so `&a.b`, but in NPL, the use of this `(&a).b` expression is more prevalent than the use of this `&(a.b)` expression, so, the precedence level of NPL is designed to favour the entry of the more prevalent expression without precedence entry like so `&a.b`. The reason why `(&a).b` is the prevalent expression can be inferred from the semantic section when read.

##### Associativity

While precedence defines the order of which operators evaluate their operands first, associativity defines the order of evaluation when operators of the same precedence are involved in the same expression. The order associativity defines is always **left to right** or **right to left**, with a **left to right** associativity starting operator evaluation of their operands from the *left* and the **right to left** associativity starting operator evaluation of their operands from the *right*, an example `2 + 3 - 4 - 9` would be interpreted as follows, the language gives additive operators (_`+` & `-`_) a left to right associativity, so the following would be evaluated like this `(((2 + 3) - 4) - 9)` which results in  `-8`, having a right to left associativity instead would make it to be evaluated like this `(2 + (3 - (4 - 9)))` which results in `10` . In NPL, all associativity of operators of the same precedence level are **left to right** except for prefix operators which are **right to left** for good reason. And like with precedence levels, the layout of the primary expressions syntax is also setup to identify associativity. It works by simply calling the higher precedence level as the RHS for binary expressions to achieve **left to right** associativity, calling the the current precedence level as the RHS for binary expressions to achieve **right to left** associativity and finally calling the current precedence level after the various prefix operators as the only operand for unary postfix operators. It is logically impossible to implement **right to left** associativity for unary prefix operators. An example of changing a **left to right** associative to a **right to left** associative using `assignmentBinaryExpression`:

```json
assignmentBinaryExpression = list(logicalBinaryExpression, assignmentBinaryOperator)
```

Turning into a **right to left** associative:

```json
assignmentBinaryExpression = logicalBinaryExpression (assignmentBinaryOperator assignmentBinaryExpression)
```

Languages like C and C++ use the above because assignment binary expressions are value returning, which makes it logical for it to be **right to left** associative, for example, `a = b = c` evaluates to this `(a = (b = c))`, but since assignment binary expressions are not value returning in NPL (_would be explained in the semantic section_), it is irrelevant what associativity they get, so I chose **left to right** mostly to avoid needless recursion in code.

Implementation of associativity is a non issue because implementing precedence levels with the above guide already implements associativity.

> Note that this associativity section is not pivotal to the specification of this document, because it neither contains a problem to address nor a good practice to adhere to, it instead just serves as an educational piece for readers, most especially compiler developers, curious about the specific structure of the primary expressions syntax and what exactly associativity is.

##### White-Space dependent parsing

Using white-space information in parsing to avoid high-level syntax parsing conflicts. Some certain expression syntaxes are not unique amongst each other, their syntaxes overlap which is near impossible to parse them with certainty and this further exacerbated in syntaxes that ask for more than one expression that could span multiple lines like in block syntaxes, for example:

```
: Should the below be parsed as a collection expression with a tag and erroneous precedence entry or function call?
➜ a[b] ()

: Should the below be parsed as an identifier and expression grouping or function call?
➜ a (3, 4)

: Should the below be parsed as an identifier, collection expression without a tag and precedence entry or function call or collection expression with a tag and precedence entry?
➜ a [] (3)

: Should the below be parsed as an identifier, collection expression without a tag and expression grouping or function call or collection expression with a tag and expression grouping?
➜ a [] (4, 5, 6)

: Should the below be parsed as an identifier, collection expression without a tag and expression grouping or function call or collection expression with a tag and expression grouping and erroneous precedence entry?
➜ a [ui4] (4, 5, 6) ()

: Should the below be parsed as an identifier, collection expression without a tag, LHS expression grouping for the addition expression or LHS function call for the addition expression or collection expression with a tag and LHS expression grouping for the addition expression?
➜ a []
(4, 5) + 45
```

And so on.

Actually, in syntaxes that ask for more than one expression that could span multiple lines, this can be easily avoided in the user side by making the expression delimiter (_`;`_) compulsory after each expression, so the user/programmer is the one tasked with making sure the expressions are parsed right like so:

```
: The programmer makes the below to be a collection expression with a tag and precedence entry
➜ a[b]; ();

: The programmer makes the below to be a function call
➜ a[b] ();

: The programmer makes the below to be an identifier and expression grouping
➜ a; (3, 4);

: The programmer makes the below to a function call
➜ a (3, 4);

: The programmer makes the below to be an identifier, collection expression without a tag and precedence entry
➜ a; []; (3);

: The programmer makes the below to be a function call
➜ a [] (3);

: The programmer makes the below to be an identifier, collection expression without a tag and precedence entry
➜ a;
[];
(3);
```

But none of the above is desirable in any sane setting for two simple reason, one, it gives the programmer the prerogative to write absolutely dumb and confusing code, for example, `a [] (3)` should not be considered a function call even in syntaxes that ask for just one expression, it is dumb and undesirable, two, needing the expression delimiter after every individual expression is not pleasant and can cause code noise in extreme cases especially when a non code noise solution (_white-space_) is readily available.

So, the programming language takes such power from the programmer and defines three rules that makes use of the white-space information for the parsing of these certain high-level construct syntaxes.

###### Rules

1. Using white-space to decisively parse for collection expressions

   A collection expression with `userIdentifierToken` (that is its tag) must have an absence of white-space between the `userIdentifierToken` and the collection expression hinting tokens, that is `[`, like so:

   ```
   ➜ a[34, 5, 6]
   ➜ a[]
   ```

   Any presence of white-space between them effectively makes them non collection expression sanctioned parsing, like so:

   ```
   : The below is an identifier and collection expression without a tag(identifier)
   ➜ a [34, 5, 6]
   ```

2. Using white-space to decisively parse for function calls

   A function call must have an absence of white-space between its function call hinting tokes, that is `(`, `[` and `!`, like so:

   ```
   ➜ a[]()
   ➜ a[]!()()
   ➜ a!()()
   ➜ a()
   ```

   Any presence of white-space between them effectively makes them non function call sanctioned parsing, like so:

   ```
   : The below is an identifier, collection expression without a tag and erroneous precedence entry
   ➜ a [] ()
   
   The below is an identifier, collection expression without a tag and erroneous syntax entry starting from `!`
   ➜ a [] ! () ()
   
   The below is a collection expression with a tag and precedence entry
   ➜ a[] (34)
   ```

3. Mandatory expression delimiter (_`;`_) for expressions that share the same line

   This rule mandates that any and all expressions that share the same line must be delimited by the expression delimiter (_`;`_), this is done for readability purposes. For example:

   ```
   : Due to the above two rules, the below comprises of individual expressions that share the same line, that is an identifier, collection expression without a tag and erroneous precedence entry, so,they must be delimited by the expression delimiter
   ➜ a [] ()
   ➜ a; []; ()
   
   : Leaving expressions like the below clear and readable
   ➜ a[]
   (34, 45) + 90
   ```

   This rule is obviously only for syntaxes that ask for more than one expression.

> Note that rules 1 and 2 could actually be represented in NTPL by using its no white-space operator to ask for the absence of white-space when parsing collection expressions and function calls like some syntaxes already do, but it is just more proper to explain here in textual format than to represent in NTPL.

###### Gap In The Rules

The above rules do not still protect from syntaxes that make use of the same operator but in different positions, like the `-` which is both a binary and unary prefix operator. For this, the user/programmer is meant to show intent of what exactly is desired to be parsed like. An example like the below:

```
➜ 2
-2

➜ 2 -
2

➜ 2     -2
```

All the above is parsed as a binary expression, but the programmer can choose to delimit the above to parse instead as either a binary expression or unary prefix expression, like so:

```
➜ 2;
-2

➜ 2 -
2

➜ 2;	-2
```

###### Reason Why I designed NPL With Such Syntax Conflicts In The First Place

I did it to keep with the conventional syntaxes in the programming and mathematical space, mainly because the conventional syntaxes are sane and intuitive to reason about, for example, it is easier to imagine an array syntax - *and by extension collection expressions* - like so `[1, 2, 3]` in programming because popular programming languages like python, javascript and PHP already set precedence for this and it is easier to imagine a function call syntax like this `foo()` because the popular procedural and imperative programming languages make use of such syntax and it is also easier to imagine the precedence entry syntax like this `(2 + 3) * 4` because years of precedence has already been set in mathematics and subsequently, in programming. Grouping syntax - *and by extension expressions grouping syntax* - is the odd ball here as I could have literally made it start with any other brace, but the reason I stuck with `()` is because it was more available (*caused lesser syntax conflicts*) than the other symbol token ASCII braces and using a non ASCII brace, like this `〈〉` or this `❴❵`, simply isn't as easy to type as this `()` or even using a combination of a unicode character and a left brace, like this `%()` or this `$()`, is too verbose and ugly for my liking, so ultimately it came down to ergonomics and my design preference.

### Block Syntax

Below is the block syntax written in NTPL:

```json
block = '{' blockID? (blockConentPart|(expression ';'?)|statement|import)* '}'
```

Auxiliary syntaxes for block syntax: written in NTPL

```json
blockID = '.' userIdentifierToken

blockContentPart = attributeLCI? function|marco|typeCreators|object|scope
```

#### Supplementary Info

Syntaxes, like `function`, `marco`, `ifConditionalExpression` and `forLoopStatement`,  that ask for the block syntax must share the same line as the calling syntax, for example:

```rust
➜ fn foo() {}

➜ fn foo() {
}

➜ if true {}

➜ if true {
}

➜ for i in [3, 4, 5] {}

➜ for i in [3, 4, 5] {
}
```

This is done to centralize the programming style of brace writing when it comes to those syntaxes which ends debates on which is the better style to use therefore ensuring universality in all NPL codebases.

### Statement Syntax

Below is the statement syntax written in NTPL:

```json
statement = loopStatement|jumpStatement
```

Secondary syntaxes for statement syntax written in NTPL:

```json
jumpStatement = '->' blockId? 'break'|'continue'|expression

loopStatement = attributeLCI? forLoopStatement|whileLoopStatement
```

Auxiliary syntaxes for statement syntax written in NTPL:

```json
forLoopStatement = 'for' (list((attributeLCI? object)) ';')? userIdentifierToken 'in' expression block

whileLoopStatement = 'while' (list((attributeLCI? object)) ';')? expression? (';' expression)? block
```

### LCIs Syntax

Below are the LCIs syntax written in NTPL:

```json
attributeLCI = 'at:'.(attributeLCIPart|grouping(atrributeLCIPart))

expressionLCI = 'exp:'.(userIdentifierToken|grouping(userIdentifierToken))

typeLCI = 'ty:'.(userIdentifierToken (valueArgumentEntry|typeArgumentEntry)?)

miscLCI = 'misc:'.(userIdentifierToken valueArgumentEntry)
```

Auxiliary syntaxes for LCI syntax written in NTPL:

```json
attributeLCIPart = userIdentifierToken attributeLCIArgumentEntry?
```

### Import Syntax

Below is the import syntax written in NTPL:

```json
import = 'import' 'mod'|'pkg'|'lib'|'type'|'scope'|'fn'|'marco'|'contract'|'obj' scopedIdentifier|grouping(scopedIdentifier)
```

### Use Syntax

Below is the use syntax written in NTPL:

```json
use = 'use' ('impl'|'fn'|'obj'|'field'|'scope' userIdentifierToken|grouping(userIdentifierToken))|useForMarco|'*'
```

Auxiliary syntaxes for use syntax written in NTPL:

```json
useForMarco = 'marco' userIdentifierToken|miscLCI|grouping(userIdentifierToken|miscLCI)
```

### Groupings Syntax

Below are the groupings syntax written in NTPL:

```json
grouping($exp:exp) = '('list($exp, _, `{2,}`)')'

objectGrouping = 'mut'? grouping(mainObjectPart) (objectTypeEntry|indirectInit)?

valueParameterGrouping = '..'? 'mut'? grouping(basicValueParameter|variadicValueParameter) (':' '..'? type)?

functionExpressionValueParameterGrouping = 'mut'? grouping(functionExpressionValueParameterPart) (':' type)?

fieldGrouping = '..'? 'mut'? grouping(basicField|variadicField) (':' '..'? type)?
```

#### Supplementary Info

Some high-level construct syntaxes have different ways grouping can be applied to them, they are called grouping versions, and a grouping version is **not allowed** to be entered with another grouping version. Because grouping is syntactic feature (*Would be explained in the semantic section*), all grouping syntax conflicts must be resolved at the syntax level.

Objects are such high-level constructs that have grouping versions. The various objects grouping syntaxes were written in a generic way to accommodate all acceptable grouping versions of the objects grouping format because it was deemed better to parse all allowed grouping versions first then scrutinize after. The following information would detail the rules on how to separate the various grouping versions from each other:

- Rule **1**

  If a `mut` is entered outside the grouping, then no `mut` should be found inside the grouping. For example:
  
  ```
  : The below is illegal
  ➜ obj mut (mut x, y)
  ```
  
  Applicable to `object`, `valueParameter`, `functionExpressionValueParameter` and `field`.
  
- Rule **2**

  If a `type` with initialization, that is `directInit` or `indirectInit`, is entered inside the grouping, then no `type` with initialization (1), type without initialization (2) and initialization (3) should be found outside the grouping. For example:

  ```
  : The below is illegal (1)
  ➜ obj (x: si4(), y: si8): si4()
  
  : The below is illegal (2)
  ➜ obj (x: si4 = 0, y: si8): si4
  
  : The below is illegal (3)
  ➜ obj (x: si4(), y: si8) = 90 obj (x: si5, y): si4
  ```

  Applicable to `object` and `valueParameter`, with `valueParameter`'s syntax taken into consideration, meaning that even though `valueParameter` parses for a specific type of initialization, the rule still applies to it.

- Rule **3**

  If a type without initialization, that is `directInit` or `indirectInit`, is entered inside the grouping, then no `type` with initialization (1) and `type` without initialization (2) should be found outside the grouping. For example:

  ```
  : The below is illegal (1)
  ➜ obj (x: si4, y): si4 = 45
  
  : The below is illegal (2)
  ➜ obj (x: si4, y): si4
  ```

  Applicable to `object`, `valueParameter`, `functionExpressionValueParameter` and `fields`, with their specific syntaxes taken into consideration, meaning that even though some objects syntaxes like `field`s, for example, do not parse for initialization, the rule still applies to it.

- Rule **4**

  If an initialization, that is `directInit` or `indirectInit`, is entered inside the grouping, then no `type` with initialization (1), type without initialization (2) and initialization (3) should be found outside the grouping. For example:

  ```
  : The below is illegal (1)
  ➜ obj (x, y = 9): si4()
  
  : The below is illegal (2)
  ➜ obj (x, y = 9): si4
  
  : The below is illegal (3)
  ➜ obj (x, y = 9) = 90
  ```

  Applicable to `object` and `valueParameter`, with `valueParameter`'s syntax taken into consideration, meaning the same thing as stated in Rule **2**.

- Rule **5**

  If  `..` is entered outside the grouping, then no `..` should be found entered along an identifier inside the grouping. For example:

  ```
  : The below is illegal
  ➜ obj ..(x: si8, ..y: si4)
  ```

  Applicable to `valueParameter` and `field`.

- Rule **6**

  If `..` is entered along a type inside the grouping, then no `..` should be entered along a type outside the grouping. For example:

  ```
  : The below is illegal
  ➜ obj (..x: ..si4, y: si8): ..si8
  ```

  Applicable to `valueParameter` and `field`. Note that rule **6** is redundant due to rule **3**, it was merely stated for completeness and should not be taken seriously.

## High-Level Construct Semantic

Like was previously said, high-level construct semantic details the meaning of the various syntax, where they are expected to be, their use and their low-level implementation. Note that this section doesn't imply a one to one mapping with syntax section. But before detailing the semantics of the various high-level constructs, what exactly a high-level construct is would be discussed first.

### High-Level Constructs

Are simply the high-level abstractions used by the programming language to represent low-level concepts. They are abstractions because they abstract away the obscure implementation details of low-level concepts and present only a nicer interface for the programmer to use. Actually, although the primary purpose of the high-level abstractions are to represent low-level concepts, given the ubiquitous purpose of all high-level programming languages, it can also be used to represent the high-level concepts of other high-level programming languages by simply mapping their respective features and compiling down to them.

> Note, this high-level construct semantic section would refer to both the primary and secondary syntaxes defined in the high-level construct syntax section as formal high-level constructs.

#### Terminology

- A high-level construct is said to be **defined** when written in a code file
- A high-level construct is said to **declare** parts of its syntax

---

High-level constructs are classified into two, namely:

- Identifier high-level constructs
- Non-identifier high-level constructs

#### Identifier High-Level Constructs

Are high-level constructs that declare identifiers of their own which can then be used to refer to the high-level constructs. The following are the identifier high-level constructs:

- `contract`
- `typeCreator`
- `typeParameter`
- `objects`
- `function`
- `marco`
- `scope`

> Note that although the `impl` high-level construct declare identifiers, they aren't included as identifier high-level constructs because they actually declare identifiers of `contract` high-level constructs origin, which means they do not truly declare identifiers of their own.

There are two properties of identifier high-level constructs, namely:

- Namespace
- Scope

##### Namespace

Refers to the space where identifier high-level constructs declare their identifiers, or to simply put, namespace refers to the naming space of identifier high-level constructs.

###### Terminology and Nomenclature

- An identifier high-level construct in a namespace is said to **belong** to that namespace
- The presence of two or more identical identifiers of identifier high-level constructs in a namespace is called an **identifier conflict**

Different identifier high-level constructs belong to different namespaces with an identifier high-level construct either having its own namespace or sharing a namespace with other identifier high-level constructs.

###### Rules

- Identifier conflict is not allowed in a namespace. Meaning every identifier in a namespace must be unique, that is distinct from each other
- Identifier conflict cannot occur between identifiers of identifier high-level constructs in different namespaces

The second rule is more of an obvious statement than rule, because up until now, the rule can be implicitly inferred by the reader, but given as this is a specification document, everything must be made explicit.

Below are the namespaces in NPL:

- Contract namespace
- Type namespace
- Object namespace
- Scope namespace
- Function like namespace

###### Contract Namespace

Belongs to the `contract` identifier high-level construct.

###### Type Namespace

Belongs to all type-creators identifier high-level construct and type parameter identifier high-level construct, that is `structTypeCreator`, `unionTypeCreator`, `uniqueTypeCreator`,  `valueDefTypeCreator` and `typeParameter` all share the same namespace.

This is an amazing feature of the programming language, because unlike other high-level programming languages that have their identifiers of types sharing namespaces with identifiers of other identifier high-level constructs in the programming language, NPL is designed to have its identifiers of types belong to their very own namespace. This avoids the need to enforce or encourage writing conventions that aim to distinguish identifiers of types from other identifiers of identifier high-level constructs.

> Despite the lack of need for a writing convention, this document and my programming style still defines one "just because".
>
> The convention:
>
> Identifiers of the `typeCreators` high-level construct consisting of the unicode basic Latin script letters, that is the English alphabet letters, are to start with lowercase (*or small*) letters except when they represent an acronym or abbreviation, while identifiers of the `typeParameter` high-level construct consisting of the unicode basic Latin script letters are to start with uppercase (*or capital*) letters.

###### Object Namespace

Belongs to all objects identifier high-level construct.

###### Scope Namespace

Belongs to the scope identifier high-level construct.

###### Function Like Namespace

Belongs to both the function and marco identifier high-level construct.

##### Scope

Refers to the area where identifier high-level constructs live or to put it in another way, scope refers to the location where identifier high-level constructs reside.

###### Terminology

- An identifier high-level construct in a scope is said to **live** or **reside** in that scope

Because the identifier high-level constructs reside in a scope, identifier high-level constructs that belong to the same namespace but live in different scopes **cannot have** identifier conflict.

An analogy to show the relation between scopes and namespaces: *Imagine scopes as houses and namespaces as rooms in those houses*.

There are two properties of scope, namely:

- Scope access
- Scope visibility

###### Scope Access

- How will I fit scope types (block scope, field scope, global scope and user defined scope)?

- How will scope access be defined and 

###### Scope Visibility

refers to the range at which the identifiers of identifier high-level construct can be seen and therefore used within a scope, or to simply put, scope visibility refers to the visibility range of identifiers of identifier high-level constructs.

###### Markdown Limitation

Due to the limitation of the markdown and HTML syntax not having headings less than `h6`, the following would headings although under the scope visibility section would be given the `h6` heading.

---

There are two types of scope visibility, namely:

- Universal scope visibility

- On definition scope visibility

###### Universal Scope Visibility

In this type of scope visibility, the visibility range starts from the start to the end of the scope it lives in. Meaning the identifier high-level construct can be used everywhere within the scope regardless of where it was defined in the scope.

The following identifier high-level constructs make use of this type of scope visibility:

- `contract`
- `typeCreators`
- `scope`
- `function`
- `marco`

###### On Definition Scope Visibility

In this type of scope visibility, the visibility range starts from when the high-level construct is defined to the end of the scope it lives in.

The following identifier high-level constructs make use of this type of scope visibility:

- `typeParameter`
- `objects`

The restriction of this visibility is mandated to be invasive so as to prevent every and all attempts to use an identifier of identifier high-level construct with on definition scope visibility. Because of that, the language defines all possible cases of attempts to use identifiers of identifier high-level construct with on definition scope visibility as 

	obj a = fcn()
	obj b = 34
	
	fn fcn() si4 {
		b
	}



#### Non-Identifier High-Level Constructs

Are high-level constructs that not declare identifiers of their own. All high-level constructs that are not identifier high-level constructs are non-identifier high-level constructs.

The inclusion of non-identifier high-level constructs as a classification of high-level constructs is merely for completeness purposes other than semantic importance. So, there is simply no explanation to give other than the superficial one already stated above.





High-level concepts

- References
- Lifetimes
- Constructors
- Polymorphism
- Constraint application
- Failure handling types
- Zero sized types
- Comptime
- Value unpacking
- Type system
- Language generic string interface

### Grouping

Is a syntactic feature that allows the entry of multiple high-level constructs in a single entry. It achieves this through encapsulation of the whole high-level construct or part of the high-level construct that is representative of the whole and then allows the entry of **two or more** whole or part of that high-level construct in the encapsulation, an example of said statement would be:

```
: Whole high-level construct (expressions)
➜ {
	x = 3
	y = 5
	z = 6
}
: Turns into the below with groupings
➜ (x, y, z) = (3, 5, 6)


: Part of the high-level construct that is representative of the whole (structTypeCreator)
➜ {
	struct person = obj name: &str
	struct customer = obj name: &str
}
: Turns into the below with groupings, with the "part" being the struct's identifier
➜ struct (person, customer) = obj name: &str
```

It's main inclusion in the programming language is to eliminate unnecessary typing that sometimes leads to code verbosity and to add a more high-level touch to the programming language.

##### Grouping and Expansion Semantics

Grouping semantics 