# 어휘 구조 (Lexical Structure)

<!--
The lexical structure of Swift describes what sequence of characters form valid tokens of the language. These valid tokens form the lowest-level building blocks of the language and are used to describe the rest of the language in subsequent chapters. A token consists of an identifier, keyword, punctuation, literal, or operator.

In most cases, tokens are generated from the characters of a Swift source file by considering the longest possible substring from the input text, within the constraints of the grammar that are specified below. This behavior is referred to as longest match or maximal munch.
-->

Swift 의 _어휘 구조 (lexical structure)_ 는 언어의 유효한 토큰을 형성하는 문자 시퀀스를 설명합니다. 이러한 유효한 토큰은 언어의 최하위 구성 요소를 형성하며 이후 챕터에서 나머지 언어를 설명하는데 사용됩니다. 토큰은 식별자 (identifier), 키워드 (keyword), 구두점 (punctuation), 리터럴 (literal), 또는 연산자 (operator) 로 구성됩니다.

대부분의 경우 토큰은 아래에 지정된 문법의 제약 조건 내에서 입력 텍스트에서 가능한 가장 긴 부분 문자열을 고려하여 Swift 소스 파일의 문자에서 생성됩니다. 이 동작을 _최장 일치 (longest match)_ 또는 _최대 뭉크 (maximal munch)_ 라고 합니다.

## 공백과 주석 (Whitespace and Comments)

<!--
Whitespace has two uses: to separate tokens in the source file and to distinguish between prefix, postfix, and infix operators (see Operators), but is otherwise ignored. The following characters are considered whitespace: space (U+0020), line feed (U+000A), carriage return (U+000D), horizontal tab (U+0009), vertical tab (U+000B), form feed (U+000C) and null (U+0000).

Comments are treated as whitespace by the compiler. Single line comments begin with // and continue until a line feed (U+000A) or carriage return (U+000D). Multiline comments begin with /* and end with */. Nesting multiline comments is allowed, but the comment markers must be balanced.

Comments can contain additional formatting and markup, as described in Markup Formatting Reference.
-->

공백에는 두가지 용도가 있습니다: 소스 파일에서 토큰을 분리하고 접두사, 접미사, 그리고 중위 연산자([연산자 (Operators)](lexical-structure.md#operators) 참조)를 구분 하는데 사용하지만 그렇지 않으면 무시됩니다. 다음 문자는 공백으로 간주합니다: 공백 (U+0020), 줄바꿈 (U+000A), 캐리지 리턴 (U+000D), 수평탭 (U+0009), 수직 (U+000B), 폼피드(U+000C) 그리고 null (U+0000).

주석은 컴파일러에 의해 공백으로 처리됩니다. 한 줄 주석은 `//` 로 시작하고 줄바꿈 (U+000A) 또는 캐리지 리턴 (U+000D) 까지 계속됩니다. 여러줄 주석은 `/*` 로 시작하고 `*/` 으로 끝납니다. 여러줄 주석을 중첩할 수 있지만 주석 마커는 균형을 이루어야 합니다.

주석은 [마크업 서식 참조 (Markup Formatting Reference)](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode\_markup\_formatting\_ref/index.html) 에 설명된 대로 추가 서식 및 마크업을 포함할 수 있습니다.

> GRAMMAR OF WHITESPACE\
> whitespace → [whitespace-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_whitespace-item) [whitespace](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_whitespace) $$_{opt}$$\
> whitespace-item → [line-break](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_line-break)\
> whitespace-item → [inline-space](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_inline-space)\
> whitespace-item → [comment](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_comment)\
> whitespace-item → [multiline-comment](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-comment)\
> whitespace-item → U+0000, U+000B, 또는 U+000C\
> line-break → U+000A\
> line-break → U+000D\
> line-break → U+000D 다음에 U+000A\
> inline-spaces → [inline-space](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_inline-space) [inline-spaces](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_inline-spaces) $$_{opt}$$\
> inline-space → U+0009 또는 U+0020\
> comment → `//` [comment-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_comment-text) [line-break](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_line-break)\
> multiline-comment → `/*` [multiline-comment-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-comment-text) `*/`\
> comment-text → [comment-text-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_comment-text-item) [comment-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_comment-text) $$_{opt}$$\
> comment-text-item → 다음을 제외한 모든 유니코드 스칼라 값 U+000A 또 U+000D\
> multiline-comment-text → [multiline-comment-text-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-comment-text-item) [multiline-comment-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-comment-text) $$_{opt}$$\
> multiline-comment-text-item → [multiline-comment](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-comment)\
> multiline-comment-text-item → [comment-text-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_comment-text-item)\
> multiline-comment-text-item → 다음을 제외한 모든 유니코드 스칼라 값 `/*` 또는 `*/`

## 식별자 (Identifiers)

<!--
Identifiers begin with an uppercase or lowercase letter A through Z, an underscore (_), a noncombining alphanumeric Unicode character in the Basic Multilingual Plane, or a character outside the Basic Multilingual Plane that isn’t in a Private Use Area. After the first character, digits and combining Unicode characters are also allowed.

Treat identifiers that begin with an underscore as internal, even if their declaration has the public access-level modifier. This convention lets framework authors mark part of an API that clients must not interact with or depend on, even though some limitation requires the declaration to be public. In addition, identifiers that begin with two underscores are reserved for the Swift compiler and standard library.

To use a reserved word as an identifier, put a backtick (`) before and after it. For example, class isn’t a valid identifier, but `class` is valid. The backticks aren’t considered part of the identifier; `x` and x have the same meaning.

Inside a closure with no explicit parameter names, the parameters are implicitly named $0, $1, $2, and so on. These names are valid identifiers within the scope of the closure.

The compiler synthesizes identifiers that begin with a dollar sign ($) for properties that have a property wrapper projection. Your code can interact with these identifiers, but you can’t declare identifiers with that prefix. For more information, see the propertyWrapper section of the Attributes chapter.
-->

_식별자 (Identifiers)_ 는 A 부터 Z 까지 대문자 또는 소문자, 언더바 (`_`), 다국어 기본 평면 (Basic Multilingual Plane) 에 조합하지 않은 영숫자 유니코드 문자 (noncombining alphanumeric Unicode character), 또는 개인 사용 영역 (Private Use Area) 에 없는 다국어 기본 평면 외부의 문자로 시작합니다. 첫번째 문자 다음에 숫자와 유니코드 조합 문자 (combining Unicode characters) 도 허용됩니다.

선언에 `public` 접근-수준 수정자가 있더라도 언더바로 시작하는 식별자는 내부 식별자로 처리합니다. 이 규칙을 통해 프레임워크 작성자는 일부 제한사항에 따라 선언이 공개되어야 하는 경우에도 클라이언트와 상호 작용하거나 의존해서는 안되는 API 의 부분을 표시할 수 있습니다. 또한 두 개의 언더바로 시작하는 식별자는 Swift 컴파일러와 표준 라이브러리 용으로 사용됩니다.

예약어 (reserved word) 를 식별자로 사용하려면 앞뒤에 백틱 (\`\`\`\`\`) 을 넣어야 합니다. 예를 들어 `class` 는 유효한 식별자가 아니지만 `class` 는 유효합니다. 백틱은 식별자의 부분으로 간주되지 않습니다: `x` 와 `x` 는 같은 의미입니다.

명시적으로 파라미터 이름이 없는 클로저 내의 파라미터는 암시적으로 `$0`, `$1`, `$2`, 등으로 지정됩니다. 이 이름은 클로저의 범위 내에서 유효한 식별자입니다.

컴파일러는 프로퍼티 래퍼 프로젝션 (property wrapper projection)이 있는 프로퍼티에 달러 기호 (`$`)로 시작하는 식별자를 합성합니다. 코드는 이 식별자와 상호작용 할 수 있지만 이 접두사로 식별자를 선언할 수 없습니다. 더 자세한 내용은 [속성 (Attributes)](attributes.md) 챕터에 [프로퍼티 래퍼 (propertyWrapper)](attributes.md#propertywrapper) 를 참고 바랍니다.

> GRAMMAR OF AN IDENTIFIER\
> identifier → [identifier-head](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier-head) [identifier-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier-characters) $$_{opt}$$\
> identifier → \` [identifier-head](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier-head) [identifier-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier-characters) $$_{opt}$$ \`\
> identifier → [implicit-parameter-name](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_implicit-parameter-name)\
> identifier → [property-wrapper-projection](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_property-wrapper-projection)\
> identifier-list → [identifier](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier) | [identifier](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier) `,` [identifier-list](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier-list)\
> identifier-head → A 부터 Z 까지 대문자 또는 소문자 identifier-head → `_`\
> identifier-head → U+00A8, U+00AA, U+00AD, U+00AF, U+00B2–U+00B5, 또는 U+00B7–U+00BA\
> identifier-head → U+00BC–U+00BE, U+00C0–U+00D6, U+00D8–U+00F6, 또는 U+00F8–U+00FF\
> identifier-head → U+0100–U+02FF, U+0370–U+167F, U+1681–U+180D, 또는 U+180F–U+1DBF\
> identifier-head → U+1E00–U+1FFF\
> identifier-head → U+200B–U+200D, U+202A–U+202E, U+203F–U+2040, U+2054, 또는 U+2060–U+206F\
> identifier-head → U+2070–U+20CF, U+2100–U+218F, U+2460–U+24FF, 또는 U+2776–U+2793\
> identifier-head → U+2C00–U+2DFF 또는 U+2E80–U+2FFF\
> identifier-head → U+3004–U+3007, U+3021–U+302F, U+3031–U+303F, 또는 U+3040–U+D7FF\
> identifier-head → U+F900–U+FD3D, U+FD40–U+FDCF, U+FDF0–U+FE1F, 또는 U+FE30–U+FE44\
> identifier-head → U+FE47–U+FFFD\
> identifier-head → U+10000–U+1FFFD, U+20000–U+2FFFD, U+30000–U+3FFFD, 또는 U+40000–U+4FFFD\
> identifier-head → U+50000–U+5FFFD, U+60000–U+6FFFD, U+70000–U+7FFFD, 또는 U+80000–U+8FFFD\
> identifier-head → U+90000–U+9FFFD, U+A0000–U+AFFFD, U+B0000–U+BFFFD, 또는 U+C0000–U+CFFFD\
> identifier-head → U+D0000–U+DFFFD 또는 U+E0000–U+EFFFD\
> identifier-character → 숫자 0 부터 9\
> identifier-character → U+0300–U+036F, U+1DC0–U+1DFF, U+20D0–U+20FF, 또는 U+FE20–U+FE2F\
> identifier-character → [identifier-head](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier-head)\
> identifier-characters → [identifier-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier-character) [identifier-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier-characters) $$_{opt}$$\
> implicit-parameter-name → `$` [decimal-digits](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-digits)\
> property-wrapper-projection → `$` [identifier-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier-characters)

## 키워드와 구두점 (Keywords and Punctuation)

<!--
The following keywords are reserved and can’t be used as identifiers, unless they’re escaped with backticks, as described above in Identifiers. Keywords other than inout, var, and let can be used as parameter names in a function declaration or function call without being escaped with backticks. When a member has the same name as a keyword, references to that member don’t need to be escaped with backticks, except when there’s ambiguity between referring to the member and using the keyword—for example, self, Type, and Protocol have special meaning in an explicit member expression, so they must be escaped with backticks in that context.

* Keywords used in declarations: associatedtype, class, deinit, enum, extension, fileprivate, func, import, init, inout, internal, let, open, operator, private, precedencegroup, protocol, public, rethrows, static, struct, subscript, typealias, and var.
* Keywords used in statements: break, case, catch, continue, default, defer, do, else, fallthrough, for, guard, if, in, repeat, return, throw, switch, where, and while.
* Keywords used in expressions and types: Any, as, catch, false, is, nil, rethrows, self, Self, super, throw, throws, true, and try.
* Keywords used in patterns: _.
* Keywords that begin with a number sign (#): #available, #colorLiteral, #column, #dsohandle, #elseif, #else, #endif, #error, #fileID, #fileLiteral, #filePath, #file, #function, #if, #imageLiteral, #keyPath, #line, #selector, #sourceLocation, and #warning.
* Keywords reserved in particular contexts: associativity, convenience, didSet, dynamic, final, get, indirect, infix, lazy, left, mutating, none, nonmutating, optional, override, postfix, precedence, prefix, Protocol, required, right, set, some, Type, unowned, weak, and willSet. Outside the context in which they appear in the grammar, they can be used as identifiers.

The following tokens are reserved as punctuation and can’t be used as custom operators: (, ), {, }, [, ], ., ,, :, ;, =, @, #, & (as a prefix operator), ->, `, ?, and ! (as a postfix operator).
-->

다음의 키워드는 예약되어 있으므로 [식별자 (Identifiers)](lexical-structure.md#identifiers) 에서 설명된대로 백틱을 사용하지 않는한 식별자로 사용될 수 없습니다. `inout`, `var`, 그리고 `let` 이외의 키워드는 백틱을 사용하지 않고도 함수 선언 또는 함수 호출에서 파라미터 이름으로 사용될 수 있습니다. 멤버가 키워드와 이름이 같은 경우 해당 멤버에 대한 참조는 멤버 참조와 키워드 사용 사이에 모호성이 있는 경우를 제외하고는 백틱을 사용할 필요가 없습니다—예를 들어 `self`, `Type`, 그리고 `Protocol` 은 명시적 멤버 표현식에서 특별한 의미가 있으므로 해당 컨텍스트에서 백틱을 사용해야 합니다.

* 선언에 사용되는 키워드: `associatedtype`, `class`, `deinit`, `enum`, `extension`, `fileprivate`, `func`, `import`, `init`, `inout`, `internal`, `let`, `open`, `operator`, `private`, `precedencegroup`, `protocol`, `public`, `rethrows`, `static`, `struct`, `subscript`, `typealias`, 그리고 `var`.
* 구문에 사용되는 키워드: `break`, `case`, `catch`, `continue`, `default`, `defer`, `do`, `else`, `fallthrough`, `for`, `guard`, `if`, `in`, `repeat`, `return`, `throw`, `switch`, `where`, 그리고 `while`.
* 표현식과 타입에 사용되는 키워드: `Any`, `as`, `catch`, `false`, `is`, `nil`, `rethrows`, `self`, `Self`, `super`, `throw`, `throws`, `true`, 그리고 `try`.
* 패턴에 사용되는 키워드: `_`.
* 숫자 기호 (`#`) 로 시작하는 키워드: `#available`, `#colorLiteral`, `#column`, `#dsohandle`, `#elseif`, `#else`, `#endif`, `#error`, `#fileID`, `#fileLiteral`, `#filePath`, `#file`, `#function`, `#if`, `#imageLiteral`, `#keyPath`, `#line`, `#selector`, `#sourceLocation`, 그리고 `#warning`.
* 특정 컨텍스트에서 예약된 키워드: `associativity`, `convenience`, `didSet`, `dynamic`, `final`, `get`, `indirect`, `infix`, `lazy`, `left`, `mutating`, `none`, `nonmutating`, `optional`, `override`, `postfix`, `precedence`, `prefix`, `Protocol`, `required`, `right`, `set`, `some`, `Type`, `unowned`, `weak`, 그리고 `willSet`. 컨텍스트 외부에서는 식별자로 사용될 수 있습니다.

다음 토큰은 구두점으로 예약되어 있으므로 연산자로 사용될 수 없습니다: `(`, `)`, `{`, `}`, `[`, `]`, `.`, `,`, `:`, `;`, `=`, `@`, `#`, `&` (접두사 연산자로), `->`, \`\`\`\`\`, `?`, 그리고 `!` (접미사 연산자로).

## 리터럴 (Literals)

<!--
A literal is the source code representation of a value of a type, such as a number or string.

The following are examples of literals:
-->

_리터럴 (literal)_ 은 숫자 또는 문자열과 같은 타입 값의 소스코드 표현입니다.

다음은 리터럴의 예제입니다:

```swift
42               // Integer literal
3.14159          // Floating-point literal
"Hello, world!"  // String literal
/Hello, .*/      // Regular expression literal
true             // Boolean literal
```

<!--
A literal doesn’t have a type on its own. Instead, a literal is parsed as having infinite precision and Swift’s type inference attempts to infer a type for the literal. For example, in the declaration let x: Int8 = 42, Swift uses the explicit type annotation (: Int8) to infer that the type of the integer literal 42 is Int8. If there isn’t suitable type information available, Swift infers that the literal’s type is one of the default literal types defined in the Swift standard library and listed in the table below. When specifying the type annotation for a literal value, the annotation’s type must be a type that can be instantiated from that literal value. That is, the type must conform to the Swift standard library protocols listed in the table below.
-->

리터럴은 자체 타입이 없습니다. 대신에 리터럴은 무한 정밀도를 가진 구문으로 분석되고 Swift 의 타입 추론은 리터럴에 대한 타입을 추론하려고 합니다. 예를 들어 `let x: Int8 = 42` 선언에서 Swift 는 명시적 타입 설명 (`: Int8`) 을 사용하여 정수 리터럴 `42` 가 `Int8` 의 타입이라고 유추합니다. 사용 가능한 적절한 타입 정보가 없는 경우 Swift 는 Swift 표준 라이브러리와 아래 표에서 정의된 기본 리터럴 타입 중 하나라고 유추합니다. 리터럴 값에 대한 타입 추론을 지정할 때 추론의 타입은 리터럴 값으로 부터 인스턴스될 수 있어야 합니다. 즉, 타입은 아래 표에 있는 Swift 표준 라이브러리 프로토콜을 준수해야 합니다.

|**리터럴**          |**기본타입**|**프로토콜**|
|:----------------:|:--------:|:----------------------------:|
|정수               |`Int`     |`ExpressibleByIntegerLiteral`|
|부동소수점           |`Double`  |`ExpressibleByFloatLiteral`|
|문자열              |`String`  |단일 유니코드 스칼라만 포함하는 문자열 리터럴의 경우에는 `ExpressibleByStringLiteral`, `ExpressibleByUnicodeScalarLiteral` 단일 확장 자소 클러스터 \(single extended grapheme cluster\)만 포함하는 문자열 리터럴의 경우에는 `ExpressibleByExtendedGraphemeClusterLiteral`|
|정규 표현식          |`Regex`   |None|
|불린               |`Bool`     |`ExpressibleByBooleanLiteral`|

<!--
For example, in the declaration let str = "Hello, world", the default inferred type of the string literal "Hello, world" is String. Also, Int8 conforms to the ExpressibleByIntegerLiteral protocol, and therefore it can be used in the type annotation for the integer literal 42 in the declaration let x: Int8 = 42.
-->

예를 들어, `let str = "Hello, world"` 선언에서 문자열 리터럴 `"Hello, world"` 의 추론된 타입은 기본적으로 `String` 입니다. 또한 `Int8` 은 `ExpressibleByIntegerLiteral` 프로토콜을 준수하므로 `let x: Int8 = 42` 선언에서 정수 리터럴 `42` 에 대해 해당 타입을 사용할 수 있습니다.

> GRAMMAR OF A LITERAL\
> literal → [numeric-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_numeric-literal) | [string-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_string-literal) | [regular-expression-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar_regular-expression-literal) | [boolean-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_boolean-literal) | [nil-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_nil-literal)\
> numeric-literal → `-` $$_{opt}$$ [integer-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_integer-literal) | `-` $$_{opt}$$ [floating-point-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_floating-point-literal)\
> boolean-literal → `true` | `false`\
> nil-literal → `nil`

### 정수 리터럴 (Integer Literals)

<!--
Integer literals represent integer values of unspecified precision. By default, integer literals are expressed in decimal; you can specify an alternate base using a prefix. Binary literals begin with 0b, octal literals begin with 0o, and hexadecimal literals begin with 0x.

Decimal literals contain the digits 0 through 9. Binary literals contain 0 and 1, octal literals contain 0 through 7, and hexadecimal literals contain 0 through 9 as well as A through F in upper- or lowercase.

Negative integers literals are expressed by prepending a minus sign (-) to an integer literal, as in -42.

Underscores (_) are allowed between digits for readability, but they’re ignored and therefore don’t affect the value of the literal. Integer literals can begin with leading zeros (0), but they’re likewise ignored and don’t affect the base or value of the literal.

Unless otherwise specified, the default inferred type of an integer literal is the Swift standard library type Int. The Swift standard library also defines types for various sizes of signed and unsigned integers, as described in Integers.
-->

_정수 리터럴 (Integer literals)_ 은 정밀도가 지정되지 않은 정수값을 나타냅니다. 기본적으로 정수 리터럴은 10진법으로 표현되지만 접두사를 사용하여 기준을 지정할 수 있습니다. 2진법 리터럴은 `0b` 로 시작하고, 8진법 리터럴은 `0o`, 그리고 16진법 리터럴은 `0x` 로 시작합니다.

10진법 리터럴은 `0` 부터 `9` 까지의 숫자를 포함합니다. 2진법 리터럴은 `0` 과 `1` 을 포함하고 8진법 리터럴은 `0` 부터 `7` 을 포함하고, 16진법 리터럴은 `0` 부터 `9` 뿐만 아니라 `A` 부터 `F` 까지의 대문자 또는 소문자를 포함합니다.

음의 정수 리터럴은 `-42` 와 같이 정수 리터럴 앞에 마이너스 기호 (`-`) 로 표현됩니다.

가독성을 위해 숫자 사이에 언더바 (`_`)를 허용하지만 무시되므로 리터럴 값에 영향을 주지 않습니다. 정수 리터럴은 `0` 으로 시작할 수 있지만 무시되므로 리터럴 값에 영향을 주지 않습니다.

달리 지정하지 않는 한 정수 리터럴의 기본 유추 타입은 Swift 표준 라이브러리 타입 `Int` 입니다. Swift 표준 라이브러리는 [정수 (Integers)](../language-guide-1/the-basics.md#integers) 에서 설명 했듯이 다양한 크기의 부호있는 정수와 부호없는 정수의 타입을 정의합니다.

> GRAMMAR OF AN INTEGER LITERAL\
> integer-literal → [binary-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_binary-literal)\
> integer-literal → [octal-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_octal-literal)\
> integer-literal → [decimal-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-literal)\
> integer-literal → [hexadecimal-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-literal)\
> binary-literal → `0b` [binary-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_binary-digit) [binary-literal-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_binary-literal-characters) $$_{opt}$$\
> binary-digit → 숫자 0 또는 1\
> binary-literal-character → [binary-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_binary-digit) | `_`\
> binary-literal-characters → [binary-literal-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_binary-literal-character) [binary-literal-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_binary-literal-characters) $$_{opt}$$\
> octal-literal → `0o` [octal-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_octal-digit) [octal-literal-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_octal-literal-characters) $$_{opt}$$\
> octal-digit → 숫자 0 부터 7\
> octal-literal-character → [octal-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_octal-digit) | `_`\
> octal-literal-characters → [octal-literal-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_octal-literal-character) [octal-literal-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_octal-literal-characters) $$_{opt}$$\
> decimal-literal → [decimal-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-digit) [decimal-literal-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-literal-characters) $$_{opt}$$\
> decimal-digit → 숫자 0 부터 9\
> decimal-digits → [decimal-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-digit) [decimal-digits](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-digits) $$_{opt}$$\
> decimal-literal-character → [decimal-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-digit) | `_`\
> decimal-literal-characters → [decimal-literal-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-literal-character) [decimal-literal-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-literal-characters) $$_{opt}$$\
> hexadecimal-literal → `0x` [hexadecimal-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-digit) [hexadecimal-literal-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-literal-characters) $$_{opt}$$\
> hexadecimal-digit → 숫자 0 부터 9, a 부터 f, 또는 A 부터 F\
> hexadecimal-literal-character → [hexadecimal-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-digit) | `_`\
> hexadecimal-literal-characters → [hexadecimal-literal-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-literal-character) [hexadecimal-literal-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-literal-characters) $$_{opt}$$

### 부동 소수점 리터럴 (Floating-Point Literals)

<!--
Floating-point literals represent floating-point values of unspecified precision.

By default, floating-point literals are expressed in decimal (with no prefix), but they can also be expressed in hexadecimal (with a 0x prefix).

Decimal floating-point literals consist of a sequence of decimal digits followed by either a decimal fraction, a decimal exponent, or both. The decimal fraction consists of a decimal point (.) followed by a sequence of decimal digits. The exponent consists of an upper- or lowercase e prefix followed by a sequence of decimal digits that indicates what power of 10 the value preceding the e is multiplied by. For example, 1.25e2 represents 1.25 x 102, which evaluates to 125.0. Similarly, 1.25e-2 represents 1.25 x 10-2, which evaluates to 0.0125.

Hexadecimal floating-point literals consist of a 0x prefix, followed by an optional hexadecimal fraction, followed by a hexadecimal exponent. The hexadecimal fraction consists of a decimal point followed by a sequence of hexadecimal digits. The exponent consists of an upper- or lowercase p prefix followed by a sequence of decimal digits that indicates what power of 2 the value preceding the p is multiplied by. For example, 0xFp2 represents 15 x 22, which evaluates to 60. Similarly, 0xFp-2 represents 15 x 2-2, which evaluates to 3.75.

Negative floating-point literals are expressed by prepending a minus sign (-) to a floating-point literal, as in -42.5.

Underscores (_) are allowed between digits for readability, but they’re ignored and therefore don’t affect the value of the literal. Floating-point literals can begin with leading zeros (0), but they’re likewise ignored and don’t affect the base or value of the literal.

Unless otherwise specified, the default inferred type of a floating-point literal is the Swift standard library type Double, which represents a 64-bit floating-point number. The Swift standard library also defines a Float type, which represents a 32-bit floating-point number.
-->

_부동 소수점 리터럴 (Floating-point literals)_ 은 정밀도가 지정되지 않은 부동 소수점 값을 나타냅니다.

기본적으로 부동 소수점 리터럴은 접두사 없이 10진법으로 표현되지만 `0x` 접두사를 붙여 16진법으로 표현될 수도 있습니다.

10진법 부동 소수점 리터럴은 가수 (decimal fraction), 지수 (decimal exponent) 중 하나만 있거나 둘 모두의 순서로 구성됩니다. 가수는 소수점 (`.`) 과 일련의 소수 자릿수로 구성됩니다. 지수는 대문자 또는 소문자 `e` 접두사 다음에 `e` 앞의 값에 10의 거듭 제곱을 곱한 것을 나타내는 10진수로 구성됩니다. 예를 들어 `1.25e2` 는 1.25 x 10 $$^2$$ 을 나타내고 `125.0` 입니다. 유사하게 `1.25e-2` 는 1.25 x 10 $$^{-2}$$ 를 나타내고 `0.0125` 입니다.

16진법 부동 소수점 리터럴은 `0x` 접두사 다음으로 선택적으로 지수 (hexadecimal exponent) 뒤에 가수 (hexadecimal fraction) 으로 구성됩니다. 가수는 소수점과 일련의 16진수로 구성됩니다. 지수는 대문자 또는 소문자 `p` 접두사 다음에 `p` 앞의 값에 2의 거듭 제곱을 곱한 것을 나타내는 10진수로 구성됩니다. 예를 들어 `0xFp2` 는 15 x 2 $$^2$$ 를 나타내고 `60` 입니다. 유사하게 `0xFp-2` 는 15 x 2 $$^{-2}$$ 를 나타내고 `3.75` 입니다.

음수 부동 소수점 리터럴은 `-42.5` 와 같이 부동 소수점 리터럴 앞에 마이너스 기호 (`-`) 를 추가하여 표현됩니다.

가독성을 위해 숫자 사이에 언더바 (`_`)를 허용하지만 무시되므로 리터럴 값에 영향을 주지 않습니다. 부동 소수점 리터럴은 `0` 으로 시작될 수 있지만 마찬가지로 무시되므로 리터럴의 기준이나 값에 영향을 주지 않습니다.

달리 지정하지 않는 한 부동 소수점 리터럴의 기본 유추 타입은 64-비트 부동 소수점 숫자인 Swift 표준 라이브러리 타입 `Double` 입니다. Swift 표준 라이브러리는 32-비트 부동 소수점 숫자인 `Float` 타입도 정의합니다.

> GRAMMAR OF A FLOATING-POINT LITERAL\
> floating-point-literal → [decimal-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-literal) [decimal-fraction](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-fraction) $$_{opt}$$ [decimal-exponent](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-exponent) $$_{opt}$$\
> floating-point-literal → [hexadecimal-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-literal) [hexadecimal-fraction](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-fraction) opt [hexadecimal-exponent](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-exponent)\
> decimal-fraction → `.` [decimal-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-literal)\
> decimal-exponent → [floating-point-e](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_floating-point-e) [sign](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_sign) $$_{opt}$$ [decimal-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-literal)\
> hexadecimal-fraction → `.` [hexadecimal-digit](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-digit) [hexadecimal-literal-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_hexadecimal-literal-characters) $$_{opt}$$\
> hexadecimal-exponent → [floating-point-p](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_floating-point-p) [sign](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_sign) $$_{opt}$$ [decimal-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_decimal-literal)\
> floating-point-e → `e` | `E`\
> floating-point-p → `p` | `P`\
> sign → `+` | `-`

### 문자열 리터럴 (String Literals)

<!--
A string literal is a sequence of characters surrounded by quotation marks. A single-line string literal is surrounded by double quotation marks and has the following form:
-->

문자열 리터럴은 따옴표로 묶인 일련의 문자입니다. 한 줄 문자열 리터럴은 쌍따옴표로 묶이며 형식은 다음과 같습니다:

![](<../.gitbook/assets/스크린샷 2021-02-21 오후 3.01.37.png>)

<!--
String literals can’t contain an unescaped double quotation mark ("), an unescaped backslash (\), a carriage return, or a line feed.

A multiline string literal is surrounded by three double quotation marks and has the following form:
-->

문자열 리터럴은 이스케이프 처리되지 않은 (unescaped) 쌍따옴표 (`"`), 이스케이프 처리되지 않은 백슬래시 (`\`), 캐리지 리턴 또는 줄바꿈을 포함할 수 없습니다.

여러줄 문자열 리터럴은 3개의 쌍따옴표로 묶이며 형식은 다음과 같습니다:

![](<../.gitbook/assets/스크린샷 2021-02-21 오후 3.01.51.png>)

<!--
Unlike a single-line string literal, a multiline string literal can contain unescaped double quotation marks ("), carriage returns, and line feeds. It can’t contain three unescaped double quotation marks next to each other.

The line break after the """ that begins the multiline string literal isn’t part of the string. The line break before the """ that ends the literal is also not part of the string. To make a multiline string literal that begins or ends with a line feed, write a blank line as its first or last line.

A multiline string literal can be indented using any combination of spaces and tabs; this indentation isn’t included in the string. The """ that ends the literal determines the indentation: Every nonblank line in the literal must begin with exactly the same indentation that appears before the closing """; there’s no conversion between tabs and spaces. You can include additional spaces and tabs after that indentation; those spaces and tabs appear in the string.

Line breaks in a multiline string literal are normalized to use the line feed character. Even if your source file has a mix of carriage returns and line feeds, all of the line breaks in the string will be the same.

In a multiline string literal, writing a backslash (\) at the end of a line omits that line break from the string. Any whitespace between the backslash and the line break is also omitted. You can use this syntax to hard wrap a multiline string literal in your source code, without changing the value of the resulting string.

Special characters can be included in string literals of both the single-line and multiline forms using the following escape sequences:

* Null character (\0)
* Backslash (\\)
* Horizontal tab (\t)
* Line feed (\n)
* Carriage return (\r)
* Double quotation mark (\")
* Single quotation mark (\')
* Unicode scalar (\u{n}), where n is a hexadecimal number that has one to eight digits

The value of an expression can be inserted into a string literal by placing the expression in parentheses after a backslash (\). The interpolated expression can contain a string literal, but can’t contain an unescaped backslash, a carriage return, or a line feed.

For example, all of the following string literals have the same value:
-->

한 줄 문자열 리터럴과 다르게 여러줄 문자열 리터럴은 이스케이프 처리되지 않은 쌍따옴표 (`"`), 캐리지 리턴, 그리고 줄바꿈을 포함할 수 있습니다. 이스케이프 처리되지 않은 쌍따옴표 3개를 나란히 포함할 수 없습니다.

여러줄 문자열 리터럴을 시작하는 `"""` 뒤의 줄바꿈은 문자열의 부분이 아닙니다. 리터럴 종료를 나타내는 `"""` 전의 줄바꿈도 문자열의 부분이 아닙니다. 줄바꿈으로 시작하거나 끝나는 여러줄 문자열 리터럴을 만드려면 첫번째 또는 마지막 줄에 빈 줄을 작성해야 합니다.

여러줄 문자열 리터럴은 공백과 탭의 조합을 사용하여 들여쓰기 할 수 있습니다: 이 들여쓰기는 문자열에 포함되지 않습니다. 리터럴을 종료하는 `"""` 이 들여쓰기를 결정합니다: 리터럴에서 공백이 아닌 모든 줄은 닫는 `"""` 앞에 나타나는 동일한 들여쓰기로 시작해야 합니다; 탭과 공백 사이에는 변환이 없습니다. 들여쓰기 후에 추가 공백과 탭을 포함할 수 있습니다; 이러한 공백과 탭은 문자열에 나타납니다.

여러줄 문자열 리터럴의 줄바꿈은 줄바꿈 문자를 사용하는 것이 일반적입니다. 소스 파일에 캐리지 리턴과 줄바꿈이 혼합되어 있더라도 문자열의 줄바꿈은 모두 동일합니다.

여러줄 문자열 리터럴에서 줄 끝에 백슬래시 (`\`)를 작성하면 문자열에서 줄바꿈이 생략됩니다. 백슬래시와 줄바꿈 사이의 공백도 생략됩니다. 이 구문을 사용하여 결과 문자열의 값을 변경하지 않고 소스 코드에 여러줄 문자열 리터럴을 래핑할 수 있습니다.

다음 이스케이프 시퀀스를 사용하여 한 줄과 여러줄 형식의 문자열 리터럴에 특수 문자를 포함할 수 있습니다:

* Null 문자 (`\0`)
* 백슬래시 (`\\`)
* 가로 ()
* 줄바 ()
* 캐리지 리턴 ()
* 쌍따옴 (`\"`)
* 홑따옴 (`\'`)
* 유니코드 스칼 (`\u{`_n_`}`), _n_ 은 8자리 숫자로 구성된 16진법 입니다.

표현식의 값은 백슬래시 (`\`) 뒤 소괄호 안에 표현식을 위치시켜 문자열 리터럴에 삽입할 수 있습니다. 삽입된 표현식은 문자열 리터럴을 포함할 수 있지만 이스케이프 되지않은 백슬래시, 캐리지 리턴, 또는 줄바꿈을 포함할 수 없습니다.

예를 들어 아래의 문자열 리터럴은 동일한 값을 가집니다:

```swift
"1 2 3"
"1 2 \("3")"
"1 2 \(3)"
"1 2 \(1 + 2)"
let x = 3; "1 2 \(x)"
```

<!--
A string delimited by extended delimiters is a sequence of characters surrounded by quotation marks and a balanced set of one or more number signs (#). A string delimited by extended delimiters has the following forms:
-->

확장된 구분기호 (extended delimiters)로 구분된 문자열은 따옴표로 묶인 일련의 문자와 하나 이상의 숫자 기호 (`#`)의 집합입니다. 확장된 구분기호로 구분된 문자열의 형식은 다음과 같습니다:

![](<../.gitbook/assets/스크린샷 2021-02-21 오후 3.03.42.png>)

<!--
Special characters in a string delimited by extended delimiters appear in the resulting string as normal characters rather than as special characters. You can use extended delimiters to create strings with characters that would ordinarily have a special effect such as generating a string interpolation, starting an escape sequence, or terminating the string.

The following example shows a string literal and a string delimited by extended delimiters that create equivalent string values:
-->

확장된 구분기호로 구분된 문자열에서 특수문자는 일반 문자로 결과 문자열에 나타납니다. 확장된 구분기호를 사용하여 문자열 보간 생성, 이스케이프 시퀀스 시작, 또는 문자열 종료와 같은 특수 효과를 가지는 문자로 문자열을 만들 수 있습니다.

다음의 예제는 동일한 문자열 값을 생성하는 문자열 리터럴과 확장된 구분기호로 구분된 문자열을 보여줍니다:

```swift
let string = #"\(x) \ " \u{2603}"#
let escaped = "\\(x) \\ \" \\u{2603}"
print(string)
// Prints "\(x) \ " \u{2603}"
print(string == escaped)
// Prints "true"
```

<!--
If you use more than one number sign to form a string delimited by extended delimiters, don’t place whitespace in between the number signs:
-->

확장된 구분기호로 구분된 문자열에 둘 이상의 숫자 기호를 사용하는 경우 숫자 기호 사이에 공백이 있으면 안됩니다:

```swift
print(###"Line 1\###nLine 2"###) // OK
print(# # #"Line 1\# # #nLine 2"# # #) // Error
```

<!--
Multiline string literals that you create using extended delimiters have the same indentation requirements as regular multiline string literals.

The default inferred type of a string literal is String. For more information about the String type, see Strings and Characters and String.

String literals that are concatenated by the + operator are concatenated at compile time. For example, the values of textA and textB in the example below are identical—no runtime concatenation is performed.
-->

확장된 구분기호를 사용하여 생성한 여러줄 문자열 리터럴은 일반적인 여러줄 문자열 리터럴과 동일한 들여쓰기 요구사항을 가집니다.

문자열 리터럴의 기본 유추 타입은 `String` 입니다. `String` 타입에 대한 자세한 설명은 [문자열과 문자 (Strings and Characters)](../language-guide-1/strings-and-characters.md) 와 [`String`](https://developer.apple.com/documentation/swift/string) 에서 확인 가능합니다.

`+` 연산자로 연결된 문자열 리터럴은 컴파일 시 연결됩니다. 예를 들어 아래 예제의 `textA` 와 `textB` 의 값은 동일하며 런타임 연결이 수행되지 않습니다.

```swift
let textA = "Hello " + "world"
let textB = "Hello world"
```

> GRAMMAR OF A STRING LITERAL\
> string-literal → [static-string-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_static-string-literal) | [interpolated-string-literal](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_interpolated-string-literal)\
> string-literal-opening-delimiter → [extended-string-literal-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_extended-string-literal-delimiter) $$_{opt}$$ `"`\
> string-literal-closing-delimiter → `"` [extended-string-literal-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_extended-string-literal-delimiter) $$_{opt}$$\
> static-string-literal → [string-literal-opening-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_string-literal-opening-delimiter) [quoted-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_quoted-text) $$_{opt}$$ [string-literal-closing-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_string-literal-closing-delimiter)\
> static-string-literal → [multiline-string-literal-opening-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-string-literal-opening-delimiter) [multiline-quoted-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-quoted-text) $$_{opt}$$ [multiline-string-literal-closing-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-string-literal-closing-delimiter)\
> multiline-string-literal-opening-delimiter → [extended-string-literal-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_extended-string-literal-delimiter)$$_{opt}$$ `"""`\
> multiline-string-literal-closing-delimiter → `"""` [extended-string-literal-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_extended-string-literal-delimiter)$$_{opt}$$\
> extended-string-literal-delimiter → `#` [extended-string-literal-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_extended-string-literal-delimiter) $$_{opt}$$\
> quoted-text → [quoted-text-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_quoted-text-item) [quoted-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_quoted-text) $$_{opt}$$\
> quoted-text-item → [escaped-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escaped-character)\
> quoted-text-item → 다음을 제외한 모든 유니코드 스칼라 값 `"`, `\`, U+000A, 또는 U+000D\
> multiline-quoted-text → [multiline-quoted-text-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-quoted-text-item) [multiline-quoted-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-quoted-text) $$_{opt}$$\
> multiline-quoted-text-item → [escaped-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escaped-character)\
> multiline-quoted-text-item → 다음을 제외한 모든 유니코드 스칼라 값 `\`\
> multiline-quoted-text-item → [escaped-newline](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escaped-newline)\
> interpolated-string-literal → [string-literal-opening-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_string-literal-opening-delimiter) [interpolated-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_interpolated-text) $$_{opt}$$ [string-literal-closing-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_string-literal-closing-delimiter)\
> interpolated-string-literal → [multiline-string-literal-opening-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-string-literal-opening-delimiter) [multiline-interpolated-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-interpolated-text) $$_{opt}$$ [multiline-string-literal-closing-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-string-literal-closing-delimiter)\
> interpolated-text → [interpolated-text-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_interpolated-text-item) [interpolated-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_interpolated-text) $$_{opt}$$\
> interpolated-text-item → `\(` [expression](https://docs.swift.org/swift-book/ReferenceManual/Expressions.html#grammar\_expression) `)` | [quoted-text-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_quoted-text-item)\
> multiline-interpolated-text → [multiline-interpolated-text-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-interpolated-text-item) [multiline-interpolated-text](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-interpolated-text) $$_{opt}$$\
> multiline-interpolated-text-item → `\(` [expression](https://docs.swift.org/swift-book/ReferenceManual/Expressions.html#grammar\_expression) `)` | [multiline-quoted-text-item](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_multiline-quoted-text-item)\
> escape-sequence → `\` [extended-string-literal-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_extended-string-literal-delimiter)\
> escaped-character → [escape-sequence](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escape-sequence) `0` | [escape-sequence](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escape-sequence) `\` | [escape-sequence](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escape-sequence) `t` | [escape-sequence](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escape-sequence) `n` | [escape-sequence](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escape-sequence) `r` | [escape-sequence](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escape-sequence) `"` | [escape-sequence](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escape-sequence) `'`\
> escaped-character → [escape-sequence](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escape-sequence) `u` `{` [unicode-scalar-digits](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_unicode-scalar-digits) `}`\
> unicode-scalar-digits → 1-8 자리 16진수\
> escaped-newline → [escape-sequence](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_escape-sequence) [inline-spaces](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_inline-spaces) $$_{opt}$$ [line-break](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_line-break)

### 정규 표현식 리터럴 (Regular Expression Literals)

<!--
A regular expression literal is a sequence of characters surrounded by slashes (/) with the following form:
-->

정규 표현식 리터럴 \(regular expression literal\) 은 아래와 같이 슬래시 \(`/`\) 로 감싸있는 문자의 시퀀스 입니다:

![](<../.gitbook/assets/regular_expression_1.png>)

<!--
Regular expression literals must not begin with an unescaped tab or space, and they can’t contain an unescaped slash (/), a carriage return, or a line feed.

Within a regular expression literal, a backslash is understood as a part of that regular expression, not just as an escape character like in string literals. It indicates that the following special character should be interpreted literally, or that the following nonspecial character should be interpreted in a special way. For example, /\(/ matches a single left parenthesis and /\d/ matches a single digit.

A regular expression literal delimited by extended delimiters is a sequence of characters surrounded by slashes (/) and a balanced set of one or more number signs (#). A regular expression literal delimited by extended delimiters has the following forms:
-->

정규 표현식 리터럴은 탭 또는 스페이스로 시작되지 않아야 하며, 이스케이프 처리되지 않은 슬래시 \(unescaped slash\), 캐리지 리턴 \(carriage return\), 또는 줄바꿈을 포함할 수 없습니다.

정규 표현식에서의 백슬래시는 문자열 리터럴와 같이 이스케이프 문자가 아닌 정규 표현식의 부분으로 인식합니다. 백슬래시는 다음의 특수 문자는 문자 그대로 해석되거나 다음의 일반 문자는 특별한 방법으로 해석됨을 나타냅니다. 예를 들어, `/\(/` 은 단일 왼쪽 괄호이며 `/\d/` 은 단일 숫자입니다.

확장된 구분 기호로 구분된 정규 표현식 리터럴은 슬래시 \(`/`\) 로 감싸있는 문자의 시퀀스와 하나 이상의 쌍으로 숫자 기호 \(`#`\) 로 되어있습니다. 확장된 구분 기호로 구분된 정규 표현식 리터럴은 다음의 형식을 가집니다:

![](<../.gitbook/assets/regular_expression_2.png>)

<!--
A regular expression literal that uses extended delimiters can begin with an unescaped space or tab, contain unescaped slashes (/), and span across multiple lines. For a multiline regular expression literal, the opening delimiter must be at the end of a line, and the closing delimiter must be on its own line. Inside a multiline regular expression literal, the extended regular expression syntax is enabled by default—specifically, whitespace is ignored and comments are allowed.

If you use more than one number sign to form a regular expression literal delimited by extended delimiters, don’t place whitespace in between the number signs:
-->

확장된 구분 기호를 사용한 정규 표현식 리터럴은 이스케이프 처리되지 않은 스페이스 또는 탭으로 시작할 수 있고 이스케이프 처리되지 않은 슬래시 \(`/`\), 그리고 여러줄로 작성될 수 있습니다. 여러줄 정규 표현식 리터럴은 시작 구분자는 라인의 끝에 있어야 하고 끝나는 구분자는 해당 라인에 있어야 합니다. 여러줄 정규 표현식 리터럴에서 확장된 정규 표현식은 기본적으로 가능합니다—특히, 공백은 무시되고 주석은 허용됩니다.

확장된 구분자에 의해 구분된 정규 표현식 리터럴 형식에 하나 이상의 숫자 기호를 사용한다면 숫자 기호 사이에 공백이 있을 수 없습니다:

```swift
let regex1 = ##/abc/##       // OK
let regex2 = # #/abc/# #     // Error
```

<!--
If you need to make an empty regular expression literal, you must use the extended delimiter syntax.
-->

빈 정규 표현식 리터럴을 만드려면 확장된 구분자 구문을 사용해야 합니다.


> GRAMMAR OF A REGULAR EXPRESSION LITERAL\
> regular-expression-literal → [regular-expression-literal-opening-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar_regular-expression-literal-opening-delimiter) [regular-expression](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar_regular-expression) [regular-expression-literal-closing-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar_regular-expression-literal-closing-delimiter)\
> regular-expression → 모든 정규 표현식\
> regular-expression-literal-opening-delimiter → [extended-regular-expression-literal-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar_extended-regular-expression-literal-delimiter) $$_{opt}$$ `/`\
> regular-expression-literal-closing-delimiter → `/` [extended-regular-expression-literal-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar_extended-regular-expression-literal-delimiter) $$_{opt}$$\
> extended-regular-expression-literal-delimiter → `#` [extended-regular-expression-literal-delimiter](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar_extended-regular-expression-literal-delimiter) $$_{opt}$$

## 연산자 (Operators)

<!--
The Swift standard library defines a number of operators for your use, many of which are discussed in Basic Operators and Advanced Operators. The present section describes which characters can be used to define custom operators.

Custom operators can begin with one of the ASCII characters /, =, -, +, !, *, %, <, >, &, |, ^, ?, or ~, or one of the Unicode characters defined in the grammar below (which include characters from the Mathematical Operators, Miscellaneous Symbols, and Dingbats Unicode blocks, among others). After the first character, combining Unicode characters are also allowed.

You can also define custom operators that begin with a dot (.). These operators can contain additional dots. For example, .+. is treated as a single operator. If an operator doesn’t begin with a dot, it can’t contain a dot elsewhere. For example, +.+ is treated as the + operator followed by the .+ operator.

Although you can define custom operators that contain a question mark (?), they can’t consist of a single question mark character only. Additionally, although operators can contain an exclamation point (!), postfix operators can’t begin with either a question mark or an exclamation point.
-->

Swift 표준 라이브러리는 사용할 수 있는 여러가지 연산자를 정의하며 [기본 연산자 (Basic Operators)](../language-guide-1/basic-operators.md) 와 [고급 연산자 (Advanced Operators)](../language-guide-1/advanced-operators.md) 에 설명되어 있습니다. 이 섹션에서는 사용자 지정 연산자 (Custom operators)를 정의하는데 사용될 수 있는 문자를 설명합니다.

사용자 지정 연산자는 ASCII 문자 `/`, `=`, `-`, `+`, `!`, `*`, `%`, `<`, `>`, `&`, `|`, `^`, `?`, 또는 `~` 중 하나로 시작하거나 아래 문법에 정의된 유니코드 문자 중 하나로 시작할 수 있습니다 (_수학적 연산자 (Mathematical Operators)_, _기타 기호 (Miscellaneous Symbols)_ 와 딩뱃 유니코드 (Dingbats Unicode) 블럭의 문자를 포함합니다). 첫번째 문자 뒤에 유니코드 문자를 결합하는 것도 가능합니다.

점 (`.`) 으로 시작하는 사용자 지정 연산자도 정의할 수 있습니다. 이러한 연산자는 추가 점을 포함할 수 있습니다. 예를 들어 `.+.` 은 단일 연산자로 취급됩니다. 연산자가 점으로 시작하지 않으면 다른 곳에 점을 포함할 수 없습니다. 예를 들어 `+.+` 은 `+` 연산자 다음에 `.+` 연산자로 처리됩니다.

물음표 (`?`) 를 포함하여 사용자 지정 연산자를 정의할 수 있지만 단일 물음표 문자로만 구성될 수 없습니다. 또한 연산자에 느낌표 (`!`) 를 포함할 수 있지만 접미사 연산자 (postfix operators) 는 물음표나 느낌표로 시작될 수 없습니다.

<!--
NOTE
The tokens =, ->, //, /*, */, ., the prefix operators <, &, and ?, the infix operator ?, and the postfix operators >, !, and ? are reserved. These tokens can’t be overloaded, nor can they be used as custom operators.
-->

> NOTE\
> 토큰 `=`, `->`, `//`, `/*`, `*/`, `.`, 접두사 연산자 `<`, `&`, 그리고 `?`, 중위 연산자 `?`, 그리고 접미사 연산자 `>`, `!`, 그리고 `?` 는 예약되어 있습니다. 이러한 토큰은 오버로드 할 수 없으며 사용자 지정 연산자로 사용할 수 없습니다.

<!--
The whitespace around an operator is used to determine whether an operator is used as a prefix operator, a postfix operator, or an infix operator. This behavior has the following rules:

* If an operator has whitespace around both sides or around neither side, it’s treated as an infix operator. As an example, the +++ operator in a+++b and a +++ b is treated as an infix operator.
* If an operator has whitespace on the left side only, it’s treated as a prefix unary operator. As an example, the +++ operator in a +++b is treated as a prefix unary operator.
* If an operator has whitespace on the right side only, it’s treated as a postfix unary operator. As an example, the +++ operator in a+++ b is treated as a postfix unary operator.
* If an operator has no whitespace on the left but is followed immediately by a dot (.), it’s treated as a postfix unary operator. As an example, the +++ operator in a+++.b is treated as a postfix unary operator (a+++ .b rather than a +++ .b).

For the purposes of these rules, the characters (, [, and { before an operator, the characters ), ], and } after an operator, and the characters ,, ;, and : are also considered whitespace.

If the ! or ? predefined operator has no whitespace on the left, it’s treated as a postfix operator, regardless of whether it has whitespace on the right. To use the ? as the optional-chaining operator, it must not have whitespace on the left. To use it in the ternary conditional (? :) operator, it must have whitespace around both sides.

If one of the arguments to an infix operator is a regular expression literal, then the operator must have whitespace around both sides.

There’s one caveat to the rules above. If the ! or ? predefined operator has no whitespace on the left, it’s treated as a postfix operator, regardless of whether it has whitespace on the right. To use the ? as the optional-chaining operator, it must not have whitespace on the left. To use it in the ternary conditional (? :) operator, it must have whitespace around both sides.

In certain constructs, operators with a leading < or > may be split into two or more tokens. The remainder is treated the same way and may be split again. As a result, you don’t need to add whitespace to disambiguate between the closing > characters in constructs like Dictionary<String, Array<Int>>. In this example, the closing > characters aren’t treated as a single token that may then be misinterpreted as a bit shift >> operator.

To learn how to define new, custom operators, see Custom Operators and Operator Declaration. To learn how to overload existing operators, see Operator Methods.
-->

연산자 주변에 공백은 연산자가 접두사 연산자 (prefix operator), 접미사 연산자 (postfix operator), 또는 이항 연산자 (binary operator) 로 사용되는지 결정하기 위해 사용됩니다. 이 동작은 다음 규칙에 정리되어 있습니다:

* 연산자 주변 양쪽에 모두 공백이 있거나 없는 경우 이항 연산자로 처리됩니다. 예를 들어 `a+++b` 와 `a +++ b` 에 연산자 `+++` 는 이항 연산자로 처리됩니다.
* 연산자가 왼쪽에만 공백이 있다면 접두사 단항 연산자 (prefix unary operator)로 처리됩니다. 에를 들어 `a +++b` 에서 `+++` 연산자는 접두사 단항 연산자로 처리됩니다.
* 연산자가 오른쪽에만 공백이 있다면 접미사 단항 연산자 (postfix unary operator)로 처리됩니다. 예를 들어 `a+++ b` 에서 `+++` 연산자는 접미사 단항 연산자로 처리됩니다.
* 연산자 왼쪽에 공백이 없지만 바로 이어서 점 (`.`) 이 오면 접미사 단항 연산자로 처리됩니다. 예를 들어 `a+++.b` 에서 `+++` 연산자는 접미사 단항 연산자로 처리됩니다 (`a +++ .b` 가 아닌 `a+++ .b`).

이러한 규칙의 목적에 따라 연산자 앞의 문자 `(`, `[`, 그리고 `{` 연산자 뒤의 문자 `)`, `]`, 그리고 `}`, 그리고 문자 `,`, `;`, 그리고 `:` 도 공백으로 간주합니다.

미리 정의된 연산자 `!` 또는 `?` 에 왼편에 공백이 없다면 오른편에 공백 여부와 상관없이 접미사 연산자로 처리됩니다. 옵셔널 체이닝 연산자 (optional-chaining operator)로 `?` 을 사용하려면 왼편에 공백을 가지면 안됩니다. 삼항 조건부 연산자 (ternary conditional operator) (`?` `:`) 로 사용하려면 반드시 양쪽에 공백이 있어야 합니다.

중위 연산자 (infix operator)에 인자 중 하나가 정규 표현식 리터럴이라면 연산자는 양쪽에 공백을 가져야 합니다.

특정 구문에서 선행으로 `<` 또는 `>` 연산자는 둘 이상의 토큰으로 분리될 수 있습니다. 나머지는 동일한 방식으로 처리되고 다시 분리될 수 있습니다. 그 결과로 `Dictionary<String, Array<Int>>` 와 같은 구문에서 닫는 `>` 문자 사이를 명확하게 하기 위해 공백을 추가할 필요가 없습니다. 예를 들어 닫는 `>` 문자는 비트 시프트 `>>` 연산자로 잘못 해석될 수 있는 단일 토큰으로 처리되지 않습니다.

새로운 사용자 정의 연산자를 정의하는 방법을 알아보려면 [사용자 정의 연산자 (Custom Operators)](../language-guide-1/advanced-operators.md#custom-operators) 와 [연산자 선언 (Operator Declaration)](declarations.md#operator-declaration) 을 참고 바랍니다. 기존 연산자를 오버로드 하는 방법을 알아보려면 [연산자 메서드 (Operator Methods)](../language-guide-1/advanced-operators.md#operator-methods) 를 참고 바랍니다.

> GRAMMAR OF OPERATORS\
> operator → [operator-head](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_operator-head) [operator-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_operator-characters) $$_{opt}$$\
> operator → [dot-operator-head](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_dot-operator-head) [dot-operator-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_dot-operator-characters)\
> operator-head → `/` | `=` | `-` | `+` | `!` | `*` | `%` | `<` | `>` | `&` | `|` | `^` | `~` | `?`\
> operator-head → U+00A1–U+00A7\
> operator-head → U+00A9 또는 U+00AB\
> operator-head → U+00AC 또는 U+00AE\
> operator-head → U+00B0–U+00B1\
> operator-head → U+00B6, U+00BB, U+00BF, U+00D7, 또는 U+00F7\
> operator-head → U+2016–U+2017\
> operator-head → U+2020–U+2027\
> operator-head → U+2030–U+203E\
> operator-head → U+2041–U+2053\
> operator-head → U+2055–U+205E\
> operator-head → U+2190–U+23FF\
> operator-head → U+2500–U+2775\
> operator-head → U+2794–U+2BFF\
> operator-head → U+2E00–U+2E7F\
> operator-head → U+3001–U+3003\
> operator-head → U+3008–U+3020\
> operator-head → U+3030\
> operator-character → [operator-head](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_operator-head)\
> operator-character → U+0300–U+036F\
> operator-character → U+1DC0–U+1DFF\
> operator-character → U+20D0–U+20FF\
> operator-character → U+FE00–U+FE0F\
> operator-character → U+FE20–U+FE2F\
> operator-character → U+E0100–U+E01EF\
> operator-characters → [operator-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_operator-character) [operator-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_operator-characters) $$_{opt}$$\
> dot-operator-head → `.`\
> dot-operator-character → `.` | [operator-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_operator-character)\
> dot-operator-characters → [dot-operator-character](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_dot-operator-character) [dot-operator-characters](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_dot-operator-characters) $$_{opt}$$\
> binary-operator → [operator](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_operator)\
> prefix-operator → [operator](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_operator)\
> postfix-operator → [operator](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_operator)
