# Nc Programming Language Official Specification

This document defines the formal specifications of the nc programming language, the specification that would be used to write the compiler and interpreter of the nc programming language. As inferred from the previous statement, nc programming language is built to work for both compilation and an odd form of interpretation which would be discussed at length in this document. Unlike most formal specifications, this document is written in a beginner friendly way to facilitate faster understanding of the document for persons that have met the criteria of possessing rudimentary knowledge in programming concepts, NTPL and compiler development.

The official acronym of the programming language is **NPL** which stands for **<u>N</u>**c **<u>P</u>**rogramming **<u>L</u>**anguage - obviously - and the official source code file extension is `.npl`.

To describe the text representation of the nc programming language, nc's very own text processing language is used, called **nc text processing language**  and referred to as **NTPL** in this document. You are advised to read the tutorial for the text processing language before reading this document.

NPL is comprised of four basic parts, like all programming languages, which are:

1. Comments
2. Tokens
3. High-level construct syntax
4. High-level construct semantics

Comments are informal constructs ignored by the language used to convey expression of thought, intent or ideas in code, tokens are the fundamental units of the language, high-level construct syntax describe the high-level language constructs built from tokens and high-level construct semantics details the meaning of the various syntax, where they are expected to be, their use and their low-level implementation. To implement greater understanding of this document and to keep with the promise of it being written in a beginner friendly way, the four basic parts would be explained one after the other while enumerating their co-dependence.

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

Are comments that are simply discarded by the compiler and interpreter after the fact (_generally after the tokenization phase of the compiler or a special comment parsing phase before tokenization_). 

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

Are comments that are retained by the compiler and interpreter after the fact (_generally after the tokenization phase of the compiler or a special comment parsing phase before tokenization_). Reason being that document comments serve the purpose of writing documentations or meaningful text that help describe the intent of code. Therefore, all document comments are retained by the compiler and interpreter to be used in generating documentations of code when prompted by the user, further explanation would be given in the semantic section.

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
multiLineDocumentComment = '<"' .* '">'
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
- `as`
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

Are a set combination of unicode characters starting with `\` unicode character that instructs the language to perform a particular action in the text literal token. Below are the syntax list of the various text actions written in NTPL:

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
unFormattedStringTextLiteralToken = '#'{n} '"' .* '"' '#'{n}
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

---

Obviously the NTPL function for symbol tokens is `symbolToken` equal to the symbol tokens list above, but since they are too much, I am not going to write it, just imply it.

## High-Level Construct Syntax

Like was previously said, high-level construct syntax describe the high-level language constructs built from tokens. The following are the various high-level construct syntax in NPL:

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
- LCI (Language Communication Interface) syntax
- Import syntax
- Use syntax
- Groupings syntax



Needed NTPL function in this section:

```json
list($1:exp, $2:exp = ',', $3:op = `*`) = $1 ($2 $1)`$3`
```

### Format for this section

Unlike the comment and token sections, this section has a fixed format for how the information of the various syntaxes would be presented. First would be the syntax of the high-level construct in NTPL, second would be the auxiliary syntax in NTPL, if any, that would be used to display additional helper syntaxes directly linked to the high-level construct, third and finally would be the supplementary info, if any, that covers additional essential information that cannot be represented in NTPL on the parsing of the high-level construct syntax.

The format of this section shown in NTPL for fun:

```json
highLevelConstructSyntaxSection = primarySyntax auxiliarySyntax? supplementaryInfo?
```

Obviously, the above NTPL function has no real purpose in this NPL specification other than to describe the format of this section.



### Type Syntax

Below is the type syntax written in NTPL:

```json
type = basicType|functionType|contractType|valueReference|memoryAddressReferenceType|typeLCI|typeFromExpression
```

Auxiliary syntaxes for types syntax:

```json
basicType = scopedIdentifier typeArgumentEntry? comptimeValueArgumentEntry?

functionType = 'fn' '(' list(type) ')' type|'!'

contractType = '!' ('mut'? '&')? functionType|(userIdentifierToken typeArgumentEntry?)

valueReferenceType = 'mut'? '&'|'{&}' type

memoryAddressReferenceType = 'mut'? '*'|'{*}' type

typeFromExpression = '[' expression ']'
```

### Objects Syntax

Below are the objects syntax written in NTPL:

```json
object = 'obj' mainObjectPart1|mainObjectPart2|objectGrouping

valueParameter = 'obj' basicValueParameter|variadicValueParameter|valueParameterGrouping

functionExpressionValueParameter = 'obj' functionExpressionValueParameterPart|functionExpressionValueParameterGrouping

field($1:bool) = 'obj' fieldPart1|fieldPart2($1)|fieldGrouping
```

Auxiliary syntaxes for objects syntax:

```json
directInit = valueArgumentEntry

indirectInit = '=' expression

objectTypeEntry($1:bool = true) = ':' type if $1: (directInit|indirectInit)? else directInit|indirectInit

objectIdentifier = ('_'|('mut'? userIdentifierToken))|('_' userIdentifierToken)

unpackingEntry = '[' list(userIdentifierToken|'.'|unpackingEntry) ']'

mainObjectPart1 = objectIdentifier (objectTypeEntry|indirectInit)?

mainObjectPart2($1:bool = false) = 'mut'? unpackingEntry objectTypeEntry($1)|indirectInit

basicValueParameter = objectIdentifier|unpackingEntry ':' type indirectInit?

variadicValueParameter = variadicValueParameterPart ':' '..'? type

variadicValueParameterPart = ('..' 'mut'? userIdentifierToken)|('_' '..' userIdentifierToken)

fieldPart1 = '..' 'mut'? userIdentifierToken ':' '..'? type

fieldPart2($1:bool) = 'mut'? if $1: userIdentifierToken|unpackingEntry else userIdentifierToken ':' type

functionExpressionValueParameterPart = objectIdentifier|unpackingEntry (':' type)?
```

### Parameters Entry Syntax

Below are the parameters entry syntax written in NTPL:

```json
valueParameterEntry = '('list((attributeLCI? valueParameter))')'

comptimeValueParameterEntry = '!' '('list((attributeLCI? valueParameter))')'

functionExpressionValueParameterEntry = '('list(functionExpressionValueParameter)')'

typeParameterEntry = '['list(typeParameter|variadicTypeParameter)']'
```

Auxiliary syntaxes for parameters entry syntax:

```json
typeParameter = 'type' userIdentifierToken typeArgumentEntry?

variadicTypeParameter = 'type' '..' userIdentifierToken
```

### Arguments Entry Syntax

Below are the arguments entry syntax for NTPL:

```json
valueArgumentEntry = '('list(valueArgument)')'

comptimeValueArgumentEntry = '!' '('list(valueArgument)')'

typeArgumentEntry = '[' list(typeArgument) ']'
```

Auxiliary syntaxes for arguments entry syntax:

```json
valueArgument = expression|parameterValueArgument|valueArgumentListGenerator|expressionCodeArgument|'_'

parameterValueArgument = '.'userIdentifierToken '=' expression

valueArgumentListGenerator = '->>' customLoopStatement

customLoopStatement = loopStatementHead primaryExpression

loopStatementHead = forLoopStatementHead|whileLoopStatementHead

forLoopStatementHead = 'for' (list(object) ';')? userIdentifierToken 'in' expression

whileLoopStatementHead = 'while' (list(object) ';')? expression (';' expression)?

expressionCodeArgument = '~>' expression

typeArgument = attributeLCI? (type ('/'userIdentifierToken)?)|('/'userIdentifierToken)
```

### Constraint Application Syntax

Below is the NTPL format for constraint application syntax:

```json
constraintApplication = 'apply' logicalBinaryExpression|'_'
```

### Function Syntax

Below is the NTPL format for function syntax:

```json
function = 'fn' captureSpace? functionIdentifier valueParameterEntry? (type|'type'|'!')? constraintApplication? block|';'
```

Auxiliary NTPL format for function syntax:

```json
caputreSpace = '|'list(expression|(userIdentifierToken '=' expressions))'|'

functionIdentifier = userIdentifierToken|grouping(userIdentifierToken) typeParameterEntry? comptimeValueParameterEntry?
```

### Marco Syntax

Below is the NTPL format for function syntax:

```json
marco = 'marco' marcoIdentifier valueParameterEntry? (type|'type'|'!')? constraintApplication? block|';'
```

Auxiliary NTPL format for marco syntax:

```json
marcoIdentifier = userIdentifierToken|miscLCI|operator|grouping(userIdentifierToken|miscLCI|operator) typeParameterEntry? comptimeValueParameterEntry?

operator = 'operator' operator

operator = [todo]
```

### Type Creators Syntax

Below is the NTPL format for type creators syntax:

```json
typeCreator = structTypeCreator|unionTypeCreator|valueDefCreator|uniqueTypeCreator

structTypeCreator = 'struct' genericTypeCreatorIdentifier constraintApplication? ( '=' list(field(true)) )|';'

blankStructTypeCreator = 'struct' '=' list(field)

unionTypeCreator = 'union' genericTypeCreatorIdentifier constraintApplication? ( '=' list(field(false)) )|';'

valueDefTypeCreator = 'valueDef' typeParameterEntry? userIdentifierToken|grouping(userIdentifierToken) '=' list(userIdentifierToken)

uniqueTypeCreator = 'unique' genericTypeCreatorIdentifier constraintApplication? '=' type uniqueTypeCreatorRangeEntry?
```

Auxiliary NTPL format for type creators syntax:

```json
genericTypeCreatorIdentifier = userIdentifierToken|grouping(userIdentifierToken) typeParameterEntry? comptimeValueParameterEntry?

uniqueTypeCreatorRangeEntry = 'from' integerNumberLiteralToken'~'integerNumberLiteralToken
```

### Contract Syntax

Below is the NTPL format for contract syntax:

```json
contract = 'contract' typeParameterEntry contractIdentifier contractInheritancePart? constraintApplication? contractBody
```

Auxiliary NTPL format for contract syntax:

```json
contractBody = '=' (contractContentPart|import)+ 'end'

contractIdentifier = userIdentifierToken|grouping(userIdentifierToken) typeParameterEntry?

contractContentPart = attributeLCI? function|marco|blankStructTypeCreator

contractInheritancePart = ':' list(userIdentifierToken, '+')
```

### Impl Syntax

Below is the NTPL format for impl syntax:

```json
impl = 'impl' typeArgumentEntry? implIdentifier constraintApplication? implBody|';'
```

Auxiliary NTPL format for impl syntax:

```json
implIdentifier = userIdentifierToken|grouping(userIdentifierToken) typeArgumentEntry?

implContentPart = attributeLCI? function|marco

implBody = '=' (implContentPart|import)+ 'end'
```

### Scope Syntax

Below is the NTPL format for scope syntax:

```json
scope = 'scope' scopeIdentifier constraintApplication? scopeBody
```

Auxiliary NTPL format for scope syntax:

```json
scopeBody = '=' (scopeContentPart|impl|use|import)* 'end scope'

scopeIdentifier = (userIdentifierToken|typeScopeIdentifier)|scopeIdentifierGrouping

scopeContentPart = attributeLCI? function|marco|typeCreator|object|scope

typeScopeIdentifier = '@' userIdentifierToken typeParameterEntry? comptimeValueParameterEntry?
```

### Expressions Syntax

Below is the NTPL format for expressions syntax: (**Remember to make dot operators only accept scoped identifiers and grouping of scoped identifiers**)

```json
expression = attributeLCI? assignmentBinaryExpression

assignmentBinaryExpression = logicalBinaryExpression (assignmentBinaryOperator assignmentBinaryExpression)

logicalBinaryExpression = list(equalityBinaryExpression, logicalBinaryOperator)

equalityBinaryExpression = list(relationalBinaryExpression, equalityBinaryOperator)

relationalBinaryExpression = list(rangeBinaryExpression, relationalBinaryOperator)

rangeBinaryExpression = list(additiveBinaryExpression, '~'|'.~')

additiveBinaryExpression = list(multiplicativeBinaryExpression, '+'|'-')

multiplicativeBinaryExpression = list(exponentiationBinaryExpression, '*'|'/'|'%'|'/%')

exponentiationBinaryExpression = list(asBinaryExpression, '^')

asBinaryExpression = dotBinaryExpression ('as' 'exp'|'fn')*

dotBinaryExpression = list((unaryPrefixExpression unaryPostfixOperator*), '.')

unaryPrefixExpression = (unaryPrefixOperator unaryPrefixExpression)|primaryExpression

primaryExpression = collectionExpression|(':'? scopedIdentifier)|'variadic'|
expressionType|conditionalExpression|objectExpression|functionExpression|block|literal|
precedenceEntry|grouping(primaryExpression)|expressionLCI
```

Auxiliary NTPL format for expressions syntax:

```json
assignmentBinaryOperator = '='|':='|'+='|'-='|'*='|'/='|'%='|'^='|'=-'|'=/'|'=%'

logicalBinaryOperator = 'not'? 'and'|'or'|'xor'

equalityBinaryOperator = 'not'? 'eq'|'in'

relationalBinaryOperator = 'lt'|'gt' ('and'|'or' equalityBinaryOperator|'lt'|'gt')?

unaryPostfixOperator = functionCall|('.['expression']')|orFieldQueryConditionalExpression

functionCall = typeArgumentEntry? comptimeValueArgumentEntry? valueArgumentEntry

unaryPrefixOperator = '-'|'not'|('mut'? '&'|'addressof')

collectionExpression = userIdentifierToken '['list(expression)']'
                                 
predenceEntry = '('expression')'

expressionType = '@'type

scopedIdentifier = userIdentifierToken|'outer' (':' list(userIdentifierToken|'outer'|grouping(scopedIdentifier), ':'))?

objectExpression = 'obj' ':' (type valueArgumentEntry?)|grouping((type valueArgumentEntry?))

functionExpression = 'fn' captureSpace? functionExpressionValueParameterEntry type? block

conditionalExpression = ifConditionalExpression|matchConditionalExpression

ifConditionalExpression = 'if' (list(object) ';')? list((expression block), '|')) elseBranch?

matchConditionalExpression = 'match' (list(object) ';')? expression 'with' list((expression block), '|') elseBranch?

orFieldQueryConditionalExpression = '=>' list(orFieldQueryBranch, '|') elseBranch?

orFieldQueryBranch = mainOrFieldQueryBranch|('{'userIdetifierToken'}')

mainOrFieldQueryBranch = mainOrFieldQueryPart1 mainOrFieldQueryPart2? block

mainOrFieldQueryPart1 = userIdentifierToken|('{' list(userIdentifierToken, _, `+`) '}')

mainOrFieldQueryPart2 = ('('userIdentifierToken')')|('['list(userIdentifierToken)']')

elseBranch = 'else' block?
```

### Block Syntax

Below is the NTPL format for block syntax:

```json
block = '{' blockID? (blockConentPart|expression|statement|import)* '}'
```

Auxiliary NTPL format for block syntax:

```json
blockID = '.' userIdentifierToken

blockContentPart = attributeLCI? function|marco|typeCreator|object|scope
```

### Statement Syntax

Below is the NTPL format for statement syntax:

```json
statement = loopStatement|jumpStatement

jumpStatement = '->' blockId? 'break'|'continue'|expression

loopStatement = attributeLCI? forLoopStatement|whileLoopStatement
```

Auxiliary NTPL format for statements syntax:

```json
forLoopStatement = 'for' (list((attributeLCI? object)) ';')? userIdentifierToken 'in' expression block

whileLoopStatement = 'while' (list((attributeLCI? object)) ';')? expression? (';' expression)? block
```

### LCI Syntax

Below is the NTPL format for LCI syntax:

```json
attributeLCI = 'at' ':' (userIdentifierToken valueArgumentEntry?)|grouping((userIdentifierToken valueArgumentEntry?))

expressionLCI = 'exp' ':' userIdentifierToken

typeLCI = 'ty' ':' userIdentifierToken (valueArgumentEntry|typeArgumentEntry)?

miscLCI = 'misc' ':' (userIdentifierToken valueArgumentEntry)
```

### Import Syntax

Below is the NTPL format for import syntax:

```json
import = 'import' 'mod'|'pkg'|'lib'|'type'|'scope'|'fn'|'marco'|'contract'|'obj' scopedIdentifier|grouping(scopedIdentifier)
```

### Use Syntax

Below is the NTPL format for use syntax:

```json
use = 'use' ('impl'|'fn'|'obj'|'field'|'scope' userIdentifierToken|grouping(userIdentifierToken))|useForMarco|'*'
```

Auxiliary NTPL format for use syntax:

```json
useForMarco = 'marco' userIdentifierToken|miscLCI|grouping(userIdentifierToken|miscLCI)
```

### Groupings Syntax

Below is the NTPL format for groupings syntax:

```json
grouping($1:exp) = '(' list($1, _, `{2,}`) ')'

scopeIdentifierGrouping = '('scopeGroupingIdentifierEntryPart1|scopeGroupingIdentifierEntryPart2')'

objectGrouping = 'mut'? grouping(mainObjectPart1|mainObjectPart2(true)) (objectTypeEntry|indirectInit)?

valueParameterGrouping = '..'? 'mut'? grouping(basicValueParameter|variadicValueParameter) (':' '..'? type)?

functionExpressionValueParameterGrouping = 'mut'? '(' list(functionExpressionValueParameterPart, _, `{2,}`) ')' (':' type)?

fieldGrouping = '..'? 'mut'? '(' list(fieldPart1|fieldPart2, _, `{2,}`) ')' (':' '..'? type)?
```

Auxiliary NTPL format for groupings syntax:

```json
scopeIdentifierGroupingPart1 = grouping(userIdentifierToken)

scopeIdentifierGroupingPart2 = '@' grouping(userIdentifierToken) typeParameterEntry? comptimeValueParameterEntry?
```

## High-Level Construct Semantic

Like was previously said, high-level construct semantic details the meaning of the various syntax, where they are expected to be, their use and their low-level implementation. The following final section of this document specification would detail the various semantics of the **nc programming language**.

### Language File Contents

Before the various semantics of NPL are discussed, contents of an NPL source code file needs to be specified. Language file contents are the various high-level construct syntax that are allowed to be written in an NPL source code file. Below are the NTPL format of the various syntax that can be written in an NPL source code file:

- Types
- Context identifiers

```
unique r"1-32" = ui8 from 1~32
```



