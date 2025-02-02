# 타입 (Types)

<!--
In Swift, there are two kinds of types: named types and compound types. A named type is a type that can be given a particular name when it’s defined. Named types include classes, structures, enumerations, and protocols. For example, instances of a user-defined class named MyClass have the type MyClass. In addition to user-defined named types, the Swift standard library defines many commonly used named types, including those that represent arrays, dictionaries, and optional values.

Data types that are normally considered basic or primitive in other languages—such as types that represent numbers, characters, and strings—are actually named types, defined and implemented in the Swift standard library using structures. Because they’re named types, you can extend their behavior to suit the needs of your program, using an extension declaration, discussed in Extensions and Extension Declaration.

A compound type is a type without a name, defined in the Swift language itself. There are two compound types: function types and tuple types. A compound type may contain named types and other compound types. For example, the tuple type (Int, (Int, Int)) contains two elements: The first is the named type Int, and the second is another compound type (Int, Int).

You can put parentheses around a named type or a compound type. However, adding parentheses around a type doesn’t have any effect. For example, (Int) is equivalent to Int.

This chapter discusses the types defined in the Swift language itself and describes the type inference behavior of Swift.
-->

Swift 에서 명명된 타입과 복합 타입의 두가지 종류가 있습니다. _명명된 타입 (named type)_ 은 정의될 때 특정 이름을 부여할 수 있는 타입입니다. 명명된 타입은 클래스, 구조체, 열거형, 그리고 프로토콜을 포함합니다. 예를 들어 `MyClass` 라는 사용자 정의 클래스의 인스턴스는 `MyClass` 타입을 가집니다. 사용자 정의 명명된 타입 외에도 Swift 표준 라이브러리는 배열, 딕셔너리, 그리고 옵셔널 값을 나타내는 타입을 포함하여 일반적으로 사용되는 명명된 타입을 정의합니다.

데이터 타입 (Data types) 은 다른 언어에서 일반적으로 기본 또는 원시라고 간주됩니다—숫자, 문자, 그리고 문자열을 나타내는 타입—Swift 표준 라이브러리에서는 구조체를 사용하여 정의되고 구현된 타입입니다. 명명된 타입이므로 필요에 따라 프로그램에 맞게 적절하게 동작을 [확장 (Extensions)](../language-guide-1/extensions.md) 와 [확장 선언 (Extension Declaration)](declarations.md#extension-declaration) 에서 설명된대로 확장 선언을 사용하여 확장할 수 있습니다.

_복합 타입 (compound type)_ 은 Swift 언어 자체에 정의된 이름이 없는 타입입니다. 복합 타입은 함수 타입과 튜플 타입 두가지가 있습니다. 복합 타입은 명명된 타입과 다른 복합 타입을 포함할 수 있습니다. 예를 들어 튜플 타입 `(Int, (Int, Int))` 는 첫번째는 명명된 타입인 `Int`, 두번째는 다른 복합 타입 `(Int, Int)` 인 두개의 요소가 포함됩니다.

명명된 타입 또는 복합 타입을 묶을 소괄호를 넣을 수 있습니다. 그러나 타입을 묶은 소괄호는 아무런 영향을 주지 않습니다. 예를 들어 `(Int)` 는 `Int` 와 같습니다.

이 챕터에서는 Swift 언어 자체에 정의된 타입과 Swift 의 타입 추론에 대해 설명합니다.

> GRAMMAR OF A TYPE\
> type → [function-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_function-type)\
> type → [array-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_array-type)\
> type → [dictionary-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_dictionary-type)\
> type → [type-identifier](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-identifier)\
> type → [tuple-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_tuple-type)\
> type → [optional-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_optional-type)\
> type → [implicitly-unwrapped-optional-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_implicitly-unwrapped-optional-type)\
> type → [protocol-composition-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_protocol-composition-type)\
> type → [opaque-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_opaque-type)\
> type → [metatype-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_metatype-type)\
> type → [any-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_any-type)\
> type → [self-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_self-type)\
> type → `(` [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type) `)`

## 타입 주석 (Type Annotation)

<!--
A type annotation explicitly specifies the type of a variable or expression. Type annotations begin with a colon (:) and end with a type, as the following examples show:
-->

_타입 주석 (type annotation)_ 은 변수 또는 표현식의 타입을 명시적으로 지정합니다. 타입 주석은 아래 예제에서 보여주듯이 콜론 (`:`) 으로 시작하고 타입으로 끝납니다:

```swift
let someTuple: (Double, Double) = (3.14159, 2.71828)
func someFunction(a: Int) { /* ... */ }
```

<!--
In the first example, the expression someTuple is specified to have the tuple type (Double, Double). In the second example, the parameter a to the function someFunction is specified to have the type Int.

Type annotations can contain an optional list of type attributes before the type.
-->

첫번째 예제에서 표현식 `someTuple` 은 튜플 타입 `(Double, Double)` 을 갖도록 지정됩니다. 두번째 예제는 함수 `someFunction` 에 파라미터 `a` 는 타입 `Int` 를 갖도록 지정합니다.

타입 주석은 타입 앞에 타입 속성의 옵셔널 목록을 포함할 수 있습니다.

> GRAMMAR OF A TYPE ANNOTATION\
> type-annotation → `:` [attributes](https://docs.swift.org/swift-book/ReferenceManual/Attributes.html#grammar\_attributes) $$_{opt}$$ `inout` $$_{opt}$$ [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type)

## 타입 식별자 (Type Identifier)

<!--
A type identifier refers to either a named type or a type alias of a named or compound type.

Most of the time, a type identifier directly refers to a named type with the same name as the identifier. For example, Int is a type identifier that directly refers to the named type Int, and the type identifier Dictionary<String, Int> directly refers to the named type Dictionary<String, Int>.

There are two cases in which a type identifier doesn’t refer to a type with the same name. In the first case, a type identifier refers to a type alias of a named or compound type. For instance, in the example below, the use of Point in the type annotation refers to the tuple type (Int, Int).
-->

_타입 식별자 (type identifier)_ 는 명명된 타입 또는 명명된 타입 또는 복합 타입의 타입 별칭 (type alias) 를 나타냅니다.

대부분의 경우 타입 식별자는 식별자로 같은 이름의 명명된 타입을 직접 참조합니다. 예를 들어 `Int` 는 명명된 타입 `Int` 를 직접 참조하는 타입 식별자이고 타입 식별자 `Dictionary<String, Int>` 는 명명된 타입 `Dictionary<String, Int>` 를 직접 참조합니다.

타입 식별자가 동일한 이름의 타입을 참조하지 않는 두가지 경우가 있습니다. 첫번째는 타입 식별자는 명명된 타입 또는 복합 타입의 타입 별칭을 나타냅니다. 예를 들어 아래 예제에서 타입 주석에서 `Point` 의 사용은 튜플 타입 `(Int, Int)` 를 나타냅니다.

```swift
typealias Point = (Int, Int)
let origin: Point = (0, 0)
```

<!--
In the second case, a type identifier uses dot (.) syntax to refer to named types declared in other modules or nested within other types. For example, the type identifier in the following code references the named type MyType that’s declared in the ExampleModule module.
-->

두번째 경우 타입 식별자는 다른 모듈에서 선언되거나 다른 타입 내에 중첩된 명명된 타입을 참조하기 위해 점 (`.`) 구문을 사용합니다. 예를 들어 다음 코드의 타입 식별자는 `ExampleModule` 모듈에 선언된 명명된 타입 `MyType` 을 참조합니다.

```swift
var someValue: ExampleModule.MyType
```

> GRAMMAR OF A TYPE IDENTIFIER\
> type-identifier → [type-name](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-name) [generic-argument-clause](https://docs.swift.org/swift-book/ReferenceManual/GenericParametersAndArguments.html#grammar\_generic-argument-clause) opt | [type-name](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-name) [generic-argument-clause](https://docs.swift.org/swift-book/ReferenceManual/GenericParametersAndArguments.html#grammar\_generic-argument-clause) opt `.`[type-identifier](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-identifier)\
> type-name → [identifier](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier)

## 튜플 타입 (Tuple Type)

<!--
A tuple type is a comma-separated list of types, enclosed in parentheses.

You can use a tuple type as the return type of a function to enable the function to return a single tuple containing multiple values. You can also name the elements of a tuple type and use those names to refer to the values of the individual elements. An element name consists of an identifier followed immediately by a colon (:). For an example that demonstrates both of these features, see Functions with Multiple Return Values.

When an element of a tuple type has a name, that name is part of the type.
-->

_튜플 타입 (tuple type)_ 은 소괄호로 묶인 콤마로 구분된 타입의 목록입니다.

튜플 타입을 함수의 반환 타입으로 사용하여 함수가 여러값을 포함하는 단일 튜플을 반환하도록 할 수 있습니다. 튜플 타입의 요소에 이름을 지정하고 해당 이름을 사용하여 개별 요소의 값을 참조할 수도 있습니다. 요소 이름은 바로 뒤에 콜론 (`:`) 이 오는 식별자로 구성됩니다. 이러한 기능을 보여주는 예제는 [여러개의 반환값이 있는 함수 (Functions with Multiple Return Values)](../language-guide-1/functions.md#functions-with-multiple-return-values) 를 참고 바랍니다.

튜플 타입의 요소가 이름을 가지는 경우 이름은 타입의 부분입니다.

```swift
var someTuple = (top: 10, bottom: 12)  // someTuple is of type (top: Int, bottom: Int)
someTuple = (top: 4, bottom: 42) // OK: names match
someTuple = (9, 99)              // OK: names are inferred
someTuple = (left: 5, right: 5)  // Error: names don't match
```

<!--
All tuple types contain two or more types, except for Void which is a type alias for the empty tuple type, ().
-->

모든 튜플 타입은 빈 튜플 타입 인 `()` 에 대한 타입 별칭인 `Void` 를 제외하고 두 개 이상의 타입을 포함합니다.

> GRAMMAR OF A TUPLE TYPE\
> tuple-type → `(` `)` | `(` [tuple-type-element](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_tuple-type-element) `,` [tuple-type-element-list](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_tuple-type-element-list) `)`\
> tuple-type-element-list → [tuple-type-element](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_tuple-type-element) | [tuple-type-element](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_tuple-type-element) `,` [tuple-type-element-list](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_tuple-type-element-list)\
> tuple-type-element → [element-name](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_element-name) [type-annotation](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-annotation) | [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type)\
> element-name → [identifier](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier)

## 함수 타입 (Function Type)

<!--
A function type represents the type of a function, method, or closure and consists of a parameter and return type separated by an arrow (->):
-->

함수 타입 (function type) 은 함수, 메서드, 또는 클로저의 타입을 나타내고 화살표 (`->`) 로 구분된 파라미터와 반환 타입으로 구성됩니다:

![](<../.gitbook/assets/스크린샷 2021-02-21 오후 10.01.14.png>)

<!--
The parameter type is comma-separated list of types. Because the return type can be a tuple type, function types support functions and methods that return multiple values.

A parameter of the function type () -> T (where T is any type) can apply the autoclosure attribute to implicitly create a closure at its call sites. This provides a syntactically convenient way to defer the evaluation of an expression without needing to write an explicit closure when you call the function. For an example of an autoclosure function type parameter, see Autoclosures.

A function type can have variadic parameters in its parameter type. Syntactically, a variadic parameter consists of a base type name followed immediately by three dots (...), as in Int.... A variadic parameter is treated as an array that contains elements of the base type name. For instance, the variadic parameter Int... is treated as [Int]. For an example that uses a variadic parameter, see Variadic Parameters.

To specify an in-out parameter, prefix the parameter type with the inout keyword. You can’t mark a variadic parameter or a return type with the inout keyword. In-out parameters are discussed in In-Out Parameters.

If a function type has only one parameter and that parameter’s type is a tuple type, then the tuple type must be parenthesized when writing the function’s type. For example, ((Int, Int)) -> Void is the type of a function that takes a single parameter of the tuple type (Int, Int) and doesn’t return any value. In contrast, without parentheses, (Int, Int) -> Void is the type of a function that takes two Int parameters and doesn’t return any value. Likewise, because Void is a type alias for (), the function type (Void) -> Void is the same as (()) -> ()—a function that takes a single argument that’s an empty tuple. These types aren’t the same as () -> ()—a function that takes no arguments.

Argument names in functions and methods aren’t part of the corresponding function type. For example:
-->

_파라미터 타입 (parameter type)_ 은 콤마로 구분된 타입의 목록입니다. _반환 타입 (return type)_ 은 튜플 타입일 수 있기 때문에 함수 타입은 여러값을 반환하는 함수와 메서드를 지원합니다.

함수 타입 `() -> T` (여기서 `T` 는 모든 타입) 의 파라미터는 `autoclosure` 속성을 적용하여 호출 부분에서 암시적으로 클로저를 생성할 수 있습니다. 이것은 함수를 호출할 때 명시적으로 클로저를 작성할 필요없이 표현식의 평가를 연기하는 구문상 편리함을 제공합니다. 자동 클로저 함수 타입 파라미터의 예제는 [자동 클로저 (Autoclosures)](../language-guide-1/closures.md#autoclosures) 를 참고 바랍니다.

함수 타입은 _파라미터 타입_ 에 가변 파라미터 (variadic parameters) 를 가질 수 있습니다. 구문적으로 가변 파라미터는 `Int...` 와 같이 기본 타입 이름과 바로 뒤에 점 3개 (`...`) 로 구성됩니다. 가변 파라미터는 기본 타입 이름의 요소를 포함하는 배열로 처리됩니다. 예를 들어 가변 파라미터 `Int...` 는 `[Int]` 로 처리됩니다. 가변 파라미터를 사용하는 예제는 [가변 파라미터 (Variadic Parameters)](../language-guide-1/functions.md#variadic-parameters) 를 참고 바랍니다.

in-out 파라미터 (in-out parameter) 를 지정하려면 `inout` 키워드를 파라미터 타입 앞에 붙여야 합니다. `inout` 키워드로 가변 파라미터나 반환 타입으로 표시할 수 없습니다. In-out 파라미터는 [In-Out 파라미터 (In-Out Parameters)](../language-guide-1/functions.md#in-out-in-out-parameters) 에 설명되어 있습니다.

함수 타입에 파라미터가 하나만 가지고 있고 파라미터 타입이 튜플 타입인 경우 함수 타입을 작성할 때 튜플 타입을 괄호로 묶어야 합니다. 예를 들어 `((Int, Int)) -> Void` 는 튜플 타입 `(Int, Int)` 의 단일 파라미터를 가지고 값을 반환하지 않는 함수 타입입니다. 반대로 괄호가 없으면 `(Int, Int) -> Void` 는 두 개의 `Int` 파라미터를 가지고 값을 반환하지 않는 함수 타입입니다. 마찬가지로 `Void` 는 `()` 에 대한 타입 별칭 이므로 함수 타입 `(Void) -> Void` 는 `(()) -> ()` 와 같습니다—빈 튜플인 단일 인수를 가지는 함수와 같습니다. 이 타입은 `() -> ()` 와 같지 않습니다—인수를 가지지 않는 함수입니다.

함수와 메서드에 인수 이름은 해당 함수 타입의 일부가 아닙니다. 예를 들어:

```swift
func someFunction(left: Int, right: Int) {}
func anotherFunction(left: Int, right: Int) {}
func functionWithDifferentLabels(top: Int, bottom: Int) {}

var f = someFunction // The type of f is (Int, Int) -> Void, not (left: Int, right: Int) -> Void.
f = anotherFunction              // OK
f = functionWithDifferentLabels  // OK

func functionWithDifferentArgumentTypes(left: Int, right: String) {}
f = functionWithDifferentArgumentTypes     // Error

func functionWithDifferentNumberOfArguments(left: Int, right: Int, top: Int) {}
f = functionWithDifferentNumberOfArguments // Error
```

<!--
Because argument labels aren’t part of a function’s type, you omit them when writing a function type.
-->

인수 라벨은 함수 타입의 일부분이 아니므로 함수 타입을 작성할 때 생략합니다.

```swift
var operation: (lhs: Int, rhs: Int) -> Int     // Error
var operation: (_ lhs: Int, _ rhs: Int) -> Int // OK
var operation: (Int, Int) -> Int               // OK
```

<!--
If a function type includes more than a single arrow (->), the function types are grouped from right to left. For example, the function type (Int) -> (Int) -> Int is understood as (Int) -> ((Int) -> Int)—that is, a function that takes an Int and returns another function that takes and returns an Int.


Function types for functions that can throw or rethrow an error must be marked with the throws keyword. The throws keyword is part of a function’s type, and nonthrowing functions are subtypes of throwing functions. As a result, you can use a nonthrowing function in the same places as a throwing one. Throwing and rethrowing functions are described in Throwing Functions and Methods and Rethrowing Functions and Methods.

Function types for asynchronous functions must be marked with the async keyword. The async keyword is part of a function’s type, and synchronous functions are subtypes of asynchronous functions. As a result, you can use a synchronous function in the same places as an asynchronous one. For information about asynchronous functions, see Asynchronous Functions and Methods.
-->

함수 타입에 하나 이상의 화살표 (`->`) 를 포함하는 경우 함수 타입은 오른쪽에서 왼쪽으로 그룹화 됩니다. 예를 들어 함수 타입 `(Int) -> (Int) -> Int` 는 `(Int) -> ((Int) -> Int)` 로 이해됩니다—이 함수는 `Int` 를 가지며 `Int` 를 가지고 반환하는 다른 함수를 반환합니다.

에러를 발생 시키거나 다시 발생 시킬 수 있는 함수에 대한 함수 타입은 `throws` 키워드로 표시되어야 합니다. `throws` 키워드는 함수 타입의 일부분이며 던지지 않는 함수 (nonthrowing functions) 는 던지는 함수 (throwing functions) 의 하위 타입 (subtypes) 입니다. 결과적으로 던지는 함수로 같은 위치에서 던지지 않는 함수를 사용할 수 있습니다. 던지는 함수와 던지지 않는 함수는 [던지는 함수와 메서드 (Throwing Functions and Methods)](declarations.md#throwing-functions-and-methods) 와 [다시 던지는 함수와 메서드 (Rethrowing Functions and Methods)](declarations.md#rethrowing-functions-and-methods) 에 설명되어 있습니다.

비동기 함수에 대한 함수 타입은 `async` 키워드로 표시되어야 합니다. `async` 키워드는 함수의 타입의 부분이며, 동기 함수는 비동기 함수의 하위 타입 (subtypes) 입니다. 결과적으로 비동기 함수와 같은 위치에서 동기 함수를 사용할 수 있습니다. 비동기 함수에 대한 더 자세한 설명은 [비동기 함수와 메서드 (Asynchronous Functions and Methods)](declarations.md#asynchronous-functions-and-methods) 를 참고 바랍니다.

### 비이스케이프 클로저에 대한 제한사항 (Restrictions for Nonescaping Closures)

<!--
A parameter that’s a nonescaping function can’t be stored in a property, variable, or constant of type Any, because that might allow the value to escape.

A parameter that’s a nonescaping function can’t be passed as an argument to another nonescaping function parameter. This restriction helps Swift perform more of its checks for conflicting access to memory at compile time instead of at runtime. For example:
-->

비이스케이프 함수 (nonescaping function) 인 파라미터는 값이 이스케이프 될 수 있으므로 타입 `Any` 의 프로퍼티, 변수, 또는 상수에 저장될 수 없습니다.

비이스케이프 함수 인 파라미터는 다른 비이스케이프 함수 파라미터 인수로 전달될 수 없습니다. 이 제한사항은 Swift 가 런타임이 아닌 컴파일 시 메모리에 접근 충돌에 대한 검사를 더 많이 수행하는데 도움이 됩니다. 예를 들어:

```swift
let external: (() -> Void) -> Void = { _ in () }
func takesTwoFunctions(first: (() -> Void) -> Void, second: (() -> Void) -> Void) {
    first { first {} }       // Error
    second { second {}  }    // Error

    first { second {} }      // Error
    second { first {} }      // Error

    first { external {} }    // OK
    external { first {} }    // OK
}
```

<!--
In the code above, both of the parameters to takesTwoFunctions(first:second:) are functions. Neither parameter is marked @escaping, so they’re both nonescaping as a result.

The four function calls marked “Error” in the example above cause compiler errors. Because the first and second parameters are nonescaping functions, they can’t be passed as arguments to another nonescaping function parameter. In contrast, the two function calls marked “OK” don’t cause a compiler error. These function calls don’t violate the restriction because external isn’t one of the parameters of takesTwoFunctions(first:second:).

If you need to avoid this restriction, mark one of the parameters as escaping, or temporarily convert one of the nonescaping function parameters to an escaping function by using the withoutActuallyEscaping(_:do:) function. For information about avoiding conflicting access to memory, see Memory Safety.
-->

위의 코드에서 `takesTwoFunctions(first:second:)` 에 대한 두 파라미터는 모두 함수입니다. 두 파라미터 모두 `@escaping` 으로 표시되지 않으므로 결과적으로 둘다 비이스케이프 입니다.

위의 예제에서 "Error" 로 표시된 4개의 함수 호출은 컴파일러 에러를 일으킵니다. `first` 와 `second` 파라미터는 비이스케이프 함수이므로 다른 비이스케이프 함수 파라미터 인수로 전달될 수 없습니다. 반대로 "OK" 로 표시된 2개의 함수 호출은 컴파일러 에러를 발생시키지 않습니다. 이 함수 호출은 `external` 이 `takesTwoFunctions(first:second:)` 의 파라미터 중 하나가 아니므로 제한사항에 위배되지 않습니다.

제한사항을 피해야 하는 경우 파라미터 중 하나를 이스케이프로 표시하거나 `withoutActuallyEscaping(_:do:)` 함수를 이용하여 이스케이프 함수로 비이스케이프 함수 파라미터 중 하나를 임시로 변경해야 합니다. 메모리에 충돌 접근을 피하는 것에 대한 자세한 내용은 [메모리 안정성 (Memory Safety)](../language-guide-1/memory-safety.md) 를 참고 바랍니다.

> GRAMMAR OF A FUNCTION TYPE\
> function-type → [attributes](https://docs.swift.org/swift-book/ReferenceManual/Attributes.html#grammar\_attributes) $$_{opt}$$ [function-type-argument-clause](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_function-type-argument-clause) `async` $$_{opt}$$ `throws` $$_{opt}$$ `->` [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type)\
> function-type-argument-clause → `(` `)`\
> function-type-argument-clause → `(` [function-type-argument-list](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_function-type-argument-list) `...` $$_{opt}$$ `)`\
> function-type-argument-list → [function-type-argument](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_function-type-argument) | [function-type-argument](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_function-type-argument) `,` [function-type-argument-list](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_function-type-argument-list)\
> function-type-argument → [attributes](https://docs.swift.org/swift-book/ReferenceManual/Attributes.html#grammar\_attributes) $$_{opt}$$ `inout` $$_{opt}$$ [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type) | [argument-label](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_argument-label) [type-annotation](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-annotation)\
> argument-label → [identifier](https://docs.swift.org/swift-book/ReferenceManual/LexicalStructure.html#grammar\_identifier)

## 배열 타입 (Array Type)

<!--
The Swift language provides the following syntactic sugar for the Swift standard library Array<Element> type:
-->

Swift 언어는 Swift 표준 라이브러리 `Array<Element>` 타입에 대해 다음과 같은 구문을 제공합니다:

![](<../.gitbook/assets/스크린샷 2021-02-21 오후 10.05.08.png>)

<!--
In other words, the following two declarations are equivalent:
-->

다른 표현으로 다음의 두 선언도 동일합니다:

```swift
let someArray: Array<String> = ["Alex", "Brian", "Dave"]
let someArray: [String] = ["Alex", "Brian", "Dave"]
```

<!--
In both cases, the constant someArray is declared as an array of strings. The elements of an array can be accessed through subscripting by specifying a valid index value in square brackets: someArray[0] refers to the element at index 0, "Alex".

You can create multidimensional arrays by nesting pairs of square brackets, where the name of the base type of the elements is contained in the innermost pair of square brackets. For example, you can create a three-dimensional array of integers using three sets of square brackets:
-->

두 경우 모두 상수 someArray 는 문자열의 배열로 선언됩니다. 배열의 요소는 대괄호에 유효한 인덱스 값을 지정하여 서브 스크립트를 통해 접근할 수 있습니다: `someArray[0]` 는 `"Alex"` 인 인덱스 0번째 요소를 나타냅니다.

대괄호 쌍을 중첩하여 다차원 배열을 만들 수 있습니다. 여기서 요소의 기본 타입 이름은 가장 안쪽 대괄호 쌍에 포함됩니다. 예를 들어 대괄호 3쌍을 이용하여 정수의 3차원 배열을 생성할 수 있습니다:

```swift
var array3D: [[[Int]]] = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]
```

<!--
When accessing the elements in a multidimensional array, the left-most subscript index refers to the element at that index in the outermost array. The next subscript index to the right refers to the element at that index in the array that’s nested one level in. And so on. This means that in the example above, array3D[0] refers to [[1, 2], [3, 4]], array3D[0][1] refers to [3, 4], and array3D[0][1][1] refers to the value 4.

For a detailed discussion of the Swift standard library Array type, see Arrays.
-->

다차원 배열의 요소에 접근할 때 가장 왼쪽에 있는 서브 스크립트 인덱스는 배열의 가장 바깥 쪽에 있는 요소를 참조합니다. 오른쪽에 있는 다음 서브 스크립트 인덱스는 한 차원 더 들어가는 중첩된 배열의 요소를 참조합니다. 이것은 위의 예제에서 `array3D[0]` 은 `[[1, 2], [3, 4]]` 를 참조하고 `array3D[0][1]` 은 `[3, 4]` 그리고 `array3D[0][1][1]` 은 값 4를 참조합니다.

Swift 표준 라이브러리 `Array` 타입에 대한 자세한 설명은 [배열 (Arrays)](../language-guide-1/collection-types.md#arrays) 를 참고 바랍니다.

> GRAMMAR OF AN ARRAY TYPE\
> array-type → `[` [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type) `]`

## 딕셔너리 타입 (Dictionary Type)

<!--
The Swift language provides the following syntactic sugar for the Swift standard library Dictionary<Key, Value> type:
-->

Swift 언어는 Swift 표준 라이브러리 `Dictionary<Key, Value>` 타입에 대해 아래와 같은 구문을 제공합니다:

![](<../.gitbook/assets/스크린샷 2021-02-21 오후 10.07.48.png>)

<!--
In other words, the following two declarations are equivalent:
-->

다른 표현으로 다음의 두 선언도 동일합니다:

```swift
let someDictionary: [String: Int] = ["Alex": 31, "Paul": 39]
let someDictionary: Dictionary<String, Int> = ["Alex": 31, "Paul": 39]
```

<!--
In both cases, the constant someDictionary is declared as a dictionary with strings as keys and integers as values.

The values of a dictionary can be accessed through subscripting by specifying the corresponding key in square brackets: someDictionary["Alex"] refers to the value associated with the key "Alex". The subscript returns an optional value of the dictionary’s value type. If the specified key isn’t contained in the dictionary, the subscript returns nil.

The key type of a dictionary must conform to the Swift standard library Hashable protocol.

For a detailed discussion of the Swift standard library Dictionary type, see Dictionaries.
-->

두 경우 모두 상수 `someDictionary` 는 키로 문자열과 값으로 정수를 가지는 딕셔너리가 선언됩니다.

딕셔너리의 값은 대괄호에 해당 키를 지정하여 접근할 수 있습니다: `someDictionary["Alex"]` 는 키 `"Alex"` 와 연관된 값을 참조합니다. 서브 스크립트는 딕셔너리의 값 타입의 옵셔널 값을 반환합니다. 지정한 키가 딕셔너리에 포함되지 않은 경우 서브 스크립트는 `nil` 을 반환합니다.

딕셔너리의 키 타입은 Swift 표준 라이브러리 `Hashable` 프로토콜을 준수해야 합니다.

Swift 표준 라이브러리 `Dictionary` 타입의 자세한 설명은 [딕셔너리 (Dictionaries)](../language-guide-1/collection-types.md#dictionaries) 를 참고 바랍니다.

> GRAMMAR OF A DICTIONARY TYPE\
> dictionary-type → `[` [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type) `:` [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type) `]`

## 옵셔널 타입 (Optional Type)

<!--
The Swift language defines the postfix ? as syntactic sugar for the named type Optional<Wrapped>, which is defined in the Swift standard library. In other words, the following two declarations are equivalent:
-->

Swift 언어는 Swift 표준 라이브러리에 정의된 명명된 타입 `Optional<Wrapped>` 에 대해 접미사 `?` 구문을 정의합니다. 다른 표현으로 다음의 두 선언은 동일합니다:

```swift
var optionalInteger: Int?
var optionalInteger: Optional<Int>
```

<!--
In both cases, the variable optionalInteger is declared to have the type of an optional integer. Note that no whitespace may appear between the type and the ?.

The type Optional<Wrapped> is an enumeration with two cases, none and some(Wrapped), which are used to represent values that may or may not be present. Any type can be explicitly declared to be (or implicitly converted to) an optional type. If you don’t provide an initial value when you declare an optional variable or property, its value automatically defaults to nil.

If an instance of an optional type contains a value, you can access that value using the postfix operator !, as shown below:
-->

두 경우 모두 변수 `optionalInteger` 는 옵셔널 정수의 타입을 가지도록 선언됩니다. 타입과 `?` 사이에는 공백이 없을 수도 있습니다.

타입 `Optional<Wrapped>` 는 존재하거나 존재하지 않을 수 있는 값을 나타내는데 사용되는 `none` 과 `some(Wrapped)` 의 두가지 케이스가 있는 열거형입니다. 모든 타입은 명시적으로 선언되거나 옵셔널 타입으로 암시적으로 변환될 수 있습니다. 옵셔널 변수 또는 프로퍼티를 선언할 때 초기값을 제공하지 않으면 자동으로 `nil` 로 설정합니다.

옵셔널 타입의 인스턴스는 값을 포함할 경우 아래에서 보듯이 접시마 연산자 `!` 를 사용하여 값에 접근할 수 있습니다:

```swift
optionalInteger = 42
optionalInteger! // 42
```

<!--
Using the ! operator to unwrap an optional that has a value of nil results in a runtime error.

You can also use optional chaining and optional binding to conditionally perform an operation on an optional expression. If the value is nil, no operation is performed and therefore no runtime error is produced.

For more information and to see examples that show how to use optional types, see Optionals.
-->

`nil` 의 값을 가지는 옵셔널을 언래핑 하기위해 `!` 연산자를 사용하면 런타임 에러가 발생합니다.

옵셔널 표현식에 대해 조건부 수행을 위해 옵셔널 체이닝과 옵셔널 바인딩을 사용할 수도 있습니다. 값이 `nil` 인 경우에 작업은 더이상 수행되지 않으므로 런타임 에러가 발생하지 않습니다.

더 자세한 정보와 옵셔널 타입 사용에 대한 예제를 보려면 [옵셔널 (Optionals)](../language-guide-1/the-basics.md#optionals) 를 참고 바랍니다.

> GRAMMAR OF AN OPTIONAL TYPE\
> optional-type → [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type) `?`

## 암시적으로 언래핑된 옵셔널 타입 (Implicitly Unwrapped Optional Type)

<!--
The Swift language defines the postfix ! as syntactic sugar for the named type Optional<Wrapped>, which is defined in the Swift standard library, with the additional behavior that it’s automatically unwrapped when it’s accessed. If you try to use an implicitly unwrapped optional that has a value of nil, you’ll get a runtime error. With the exception of the implicit unwrapping behavior, the following two declarations are equivalent:
-->

Swift 언어는 옵셔널 타입에 접근할 때 자동으로 언래핑된 동작을 추가하기 위해 Swift 표준 라이브러리에 정의된 명명된 타입 `Optional<Wrapped>` 에 대한 접미사 `!` 구문을 정의합니다. `nil` 의 값을 가지는 옵셔널에 암시적 언래핑을 사용하려고 하면 런타임 에러가 발생합니다. 암시적 언래핑 동작을 제외하고 다음의 두 선언은 동일합니다:

```swift
var implicitlyUnwrappedString: String!
var explicitlyUnwrappedString: Optional<String>
```

<!--
Note that no whitespace may appear between the type and the !.

Because implicit unwrapping changes the meaning of the declaration that contains that type, optional types that are nested inside a tuple type or a generic type—such as the element types of a dictionary or array—can’t be marked as implicitly unwrapped. For example:
-->

타입과 `!` 사이에 공백이 포함되지 않을 수 있습니다.

암시적 언래핑은 해당 타입을 포함하는 선언의 의미를 변경하기 때문에 튜플 타입 또는 딕셔너리 또는 배열의 요소 타입과 같이 제너릭 타입 내에 중첩된 옵셔널 타입은 암시적 언래핑으로 표시할 수 없습니다. 예를 들어:

```swift
let tupleOfImplicitlyUnwrappedElements: (Int!, Int!)  // Error
let implicitlyUnwrappedTuple: (Int, Int)!             // OK

let arrayOfImplicitlyUnwrappedElements: [Int!]        // Error
let implicitlyUnwrappedArray: [Int]!                  // OK
```

<!--
Because implicitly unwrapped optionals have the same Optional<Wrapped> type as optional values, you can use implicitly unwrapped optionals in all the same places in your code that you can use optionals. For example, you can assign values of implicitly unwrapped optionals to variables, constants, and properties of optionals, and vice versa.

As with optionals, if you don’t provide an initial value when you declare an implicitly unwrapped optional variable or property, its value automatically defaults to nil.

Use optional chaining to conditionally perform an operation on an implicitly unwrapped optional expression. If the value is nil, no operation is performed and therefore no runtime error is produced.

For more information about implicitly unwrapped optional types, see Implicitly Unwrapped Optionals.
-->

암시적으로 언래핑된 옵셔널은 옵셔널 값과 동일한 Optional\<Wrapped> 타입을 가지므로 옵셔널을 사용할 수 있는 코드에서 동일한 위치에서 암시적으로 언래핑된 옵셔널을 사용할 수 있습니다. 예를 들어 옵셔널의 변수, 상수, 그리고 프로퍼티에 암시적으로 언래핑된 옵셔널의 값을 할당할 수 있고 그 반대도 가능합니다.

옵셔널과 마찬가지로 암시적으로 언래핑된 옵셔널 변수 또는 프로퍼티를 선언할 때 초기값을 제공하지 않으면 자동으로 `nil` 을 기본값으로 설정합니다.

암시적으로 언래핑된 옵셔널 표현식에 조건부로 동작을 수행하려면 옵셔널 체이닝을 사용합니다. 값이 `nil` 이라면 더이상 작업이 수행되지 않으며 런타임 에러가 발생하지 않습니다.

암시적으로 언래핑된 옵셔널 타입에 대한 자세한 정보는 [암시적으로 언래핑된 옵셔널 (Implicitly Unwrapped Optionals)](../language-guide-1/the-basics.md#implicitly-unwrapped-optionals) 를 참고 바랍니다.

> GRAMMAR OF AN IMPLICITLY UNWRAPPED OPTIONAL TYPE\
> implicitly-unwrapped-optional-type → [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type) `!`

## 프로토콜 구성 타입 (Protocol Composition Type)

<!--
A protocol composition type defines a type that conforms to each protocol in a list of specified protocols, or a type that’s a subclass of a given class and conforms to each protocol in a list of specified protocols. Protocol composition types may be used only when specifying a type in type annotations, in generic parameter clauses, and in generic where clauses.

Protocol composition types have the following form:
-->

_프로토콜 구성 타입 (protocol composition type)_ 은 지정된 프로토콜의 목록의 각 프로토콜을 준수하는 타입 또는 주어진 클래스의 하위 클래스와 지정된 프로토콜의 목록의 각 프로토콜을 준수하는 타입을 정의합니다. 프로토콜 구성 타입은 타입 주석, 제너릭 파라미터 절, 그리고 제너릭 `where` 절을 지정할 때만 사용할 수 있습니다.

프로토콜 구성 타입은 다음의 형식을 가집니다:

![](<../.gitbook/assets/스크린샷 2021-02-21 오후 10.13.31.png>)

<!--
A protocol composition type allows you to specify a value whose type conforms to the requirements of multiple protocols without explicitly defining a new, named protocol that inherits from each protocol you want the type to conform to. For example, you can use the protocol composition type ProtocolA & ProtocolB & ProtocolC instead of declaring a new protocol that inherits from ProtocolA, ProtocolB, and ProtocolC. Likewise, you can use SuperClass & ProtocolA instead of declaring a new protocol that’s a subclass of SuperClass and conforms to ProtocolA.

Each item in a protocol composition list is one of the following; the list can contain at most one class:

* The name of a class
* The name of a protocol
* A type alias whose underlying type is a protocol composition type, a protocol, or a class.

When a protocol composition type contains type aliases, it’s possible for the same protocol to appear more than once in the definitions—duplicates are ignored. For example, the definition of PQR in the code below is equivalent to P & Q & R.
-->

프로토콜 구성 타입을 사용하면 타입이 준수하려는 각 프로토콜에서 상속되는 명명된 프로토콜을 새롭게 명시적으로 정의하지 않아도 타입이 여러 프로토콜의 요구사항을 준수하는 값을 지정할 수 있습니다. 예를 들어 `ProtocolA`, `ProtocolB`, 그리고 `ProtocolC` 를 상속하는 새로운 프로토콜을 선언하는 대신 프로토콜 구성 타입 `ProtocolA & ProtocolB & ProtocolC` 를 사용할 수 있습니다. 마찬가지로 `SuperClass` 의 하위 클래스와 `ProtocolA` 를 준수하는 새로운 프로토콜을 선언하는 대신에 `SuperClass & ProtocolA` 를 사용할 수 있습니다.

프로토콜 구성 목록에 각 항목은 다음 중 하나입니다; 이 목록은 최대 하나의 클래스를 포함할 수 있습니다:

* 클래스의 이름
* 프로토콜의 이름
* 기본 타입이 프로토콜 구성 타입, 프로토콜, 또는 클래스 인 타입 별칭

프로토콜 구성 타입이 타입 별칭을 포함할 때 동일한 프로토콜이 정의에 중복해서 나타날 수 있으며 중복은 무시됩니다. 예를 들어 아래 코드에서 `PQR` 의 정의는 `P & Q & R` 과 동일합니다.

```swift
typealias PQ = P & Q
typealias PQR = PQ & Q & R
```

> GRAMMAR OF A PROTOCOL COMPOSITION TYPE\
> protocol-composition-type → [type-identifier](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-identifier) `&` [protocol-composition-continuation](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_protocol-composition-continuation)\
> protocol-composition-continuation → [type-identifier](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-identifier) | [protocol-composition-type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_protocol-composition-type)

## 불투명한 타입 (Opaque Type)

<!--
An opaque type defines a type that conforms to a protocol or protocol composition, without specifying the underlying concrete type.

Opaque types appear as the return type of a function or subscript, or the type of a property. Opaque types can’t appear as part of a tuple type or a generic type, such as the element type of an array or the wrapped type of an optional.

Opaque types have the following form:
-->

_불투명한 타입 (opaque type)_ 은 기본 타입 지정없이 프로토콜 또는 프로토콜 구성을 준수하는 타입을 정의합니다.

불투명한 타입은 함수 또는 서브 스크립트의 반환타입 또는 프로퍼티의 타입으로 나타납니다. 불투명한 타입은 배열의 요소 타입 또는 옵셔널의 래핑된 타입과 같은 튜플 타입 또는 제너릭 타입의 부분으로 나타날 수 없습니다.

불투명 타입은 다음의 형식을 가집니다:

![](<../.gitbook/assets/스크린샷 2021-02-21 오후 10.15.30.png>)

<!--
The constraint is a class type, protocol type, protocol composition type, or Any. A value can be used as an instance of the opaque type only if it’s an instance of a type that conforms to the listed protocol or protocol composition, or inherits from the listed class. Code that interacts with an opaque value can use the value only in ways that are part of the interface defined by the constraint.

Protocol declarations can’t include opaque types. Classes can’t use an opaque type as the return type of a nonfinal method.

A function that uses an opaque type as its return type must return values that share a single underlying type. The return type can include types that are part of the function’s generic type parameters. For example, a function someFunction<T>() could return a value of type T or Dictionary<String, T>.
-->

_제약조건 (constraint)_ 는 클래스 타입, 프로토콜 타입, 프로토콜 구성 타입, 또는 `Any` 입니다. 값은 나열된 프로토콜 또는 프로토콜 구성을 준수하는 타입의 인스턴스나 나열된 클래스를 상속하는 경우에만 불투명한 타입의 인스턴스로 사용될 수 있습니다. 불투명한 값과 상호작용하는 코드는 _제약조건 (constraint)_ 에 의해 정의된 인터페이스의 일부의 방식으로만 값으로 사용할 수 있습니다.

프로토콜 선언은 불투명한 타입을 포함할 수 없습니다. 클래스는 비파이널 메서드 (nonfinal method) 의 반환 타입으로 불투명한 타입을 사용할 수 없습니다.

불투명한 타입을 반환 타입으로 사용하는 함수는 단일 기본 타입을 공유하는 값을 반환해야 합니다. 반환 타입은 함수의 제너릭 타입 파라미터의 부분인 타입을 포함할 수 있습니다. 예를 들어 함수 `someFunction<T>()` 는 타입 `T` 또는 `Dictionary<String, T>` 의 값을 반환할 수 있습니다.

> GRAMMAR OF AN OPAQUE TYPE\
> opaque-type → `some` [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type)

## 메타타입 타입 (Metatype Type)

<!--
A metatype type refers to the type of any type, including class types, structure types, enumeration types, and protocol types.

The metatype of a class, structure, or enumeration type is the name of that type followed by .Type. The metatype of a protocol type—not the concrete type that conforms to the protocol at runtime—is the name of that protocol followed by .Protocol. For example, the metatype of the class type SomeClass is SomeClass.Type and the metatype of the protocol SomeProtocol is SomeProtocol.Protocol.

You can use the postfix self expression to access a type as a value. For example, SomeClass.self returns SomeClass itself, not an instance of SomeClass. And SomeProtocol.self returns SomeProtocol itself, not an instance of a type that conforms to SomeProtocol at runtime. You can call the type(of:) function with an instance of a type to access that instance’s dynamic, runtime type as a value, as the following example shows:
-->

_메타타입 타입 (metatype type)_ 은 클래스 타입, 구조체 타입, 열거형 타입, 그리고 프로토콜 타입을 포함하여 모든 타입의 타입을 나타냅니다.

클래스, 구조체, 또는 열거형 타입의 메타타입은 해당 타입의 이름 다음에 `.Type` 을 붙입니다. 런타임 시 프로토콜을 준수하는 구체적인 타입이 아닌 프로토콜 타입의 메타타입은 프로토콜의 이름 다음에 `.Protocol` 을 붙입니다. 예를 들어 클래스 타입 `SomeClass` 의 메타타입은 `SomeClass.Type` 그리고 프로토콜 `SomeProtocol` 의 메타타입은 `SomeProtocol.Protocol` 입니다.

접미사 `self` 표현식을 사용하여 타입을 값으로 접근할 수 있습니다. 예를 들어 `SomeClass.self` 는 `SomeClass` 의 인스턴스가 아닌 `SomeClass` 자체를 반환합니다. 그리고 `SomeProtocol.self` 는 런타임 시 `SomeProtocol` 을 준수하는 타입의 인스턴스가 아닌 `SomeProtocol` 자체를 반환합니다. 다음 예제와 같이 타입의 인스턴스와 함께 `type(of:)` 함수를 호출하여 해당 인스턴스의 동적으로 런타임 타입의 값으로 접근할 수 있습니다:

```swift
class SomeBaseClass {
    class func printClassName() {
        print("SomeBaseClass")
    }
}
class SomeSubClass: SomeBaseClass {
    override class func printClassName() {
        print("SomeSubClass")
    }
}
let someInstance: SomeBaseClass = SomeSubClass()
// The compile-time type of someInstance is SomeBaseClass,
// and the runtime type of someInstance is SomeSubClass
type(of: someInstance).printClassName()
// Prints "SomeSubClass"
```

<!--
For more information, see type(of:) in the Swift standard library.

Use an initializer expression to construct an instance of a type from that type’s metatype value. For class instances, the initializer that’s called must be marked with the required keyword or the entire class marked with the final keyword.
-->

자세한 내용은 Swift 표준 라이브러리에 [`type(of:)`](https://developer.apple.com/documentation/swift/2885064-type) 을 참고 바랍니다.

초기화 구문 표현식을 사용하여 해당 타입의 메타타입 값에서 타입의 인스턴스를 생성합니다. 클래스 인스턴스의 경우 호출되는 초기화 구문은 `required` 키워드로 표시거나 `final` 키워드로 전체 클래스를 표시해야 합니다.

```swift
class AnotherSubClass: SomeBaseClass {
    let string: String
    required init(string: String) {
        self.string = string
    }
    override class func printClassName() {
        print("AnotherSubClass")
    }
}
let metatype: AnotherSubClass.Type = AnotherSubClass.self
let anotherInstance = metatype.init(string: "some string")
```

> GRAMMAR OF A METATYPE TYPE\
> metatype-type → [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type) `.` `Type` | [type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type) `.` `Protocol`

## Any 타입 (Any Type)

<!--
The Any type can contain values from all other types. Any can be used as the concrete type for an instance of any of the following types:

* A class, structure, or enumeration
* A metatype, such as Int.self
* A tuple with any types of components
* A closure or function type
-->

`Any` 타입은 다른 모든 타입의 값을 포함할 수 있습니다. `Any` 는 다음 타입의 인스턴스에 대해 구체적인 타입으로 사용될 수 있습니다:

* 클래스, 구조체, 또는 열거형
* `Int.self` 와 같은 메타타입
* 모든 타입의 구성요소가 있는 튜플
* 클로저 또는 함수 타입

```swift
let mixed: [Any] = ["one", 2, true, (4, 5.3), { () -> Int in return 6 }]
```

<!--
When you use Any as a concrete type for an instance, you need to cast the instance to a known type before you can access its properties or methods. Instances with a concrete type of Any maintain their original dynamic type and can be cast to that type using one of the type-cast operators—as, as?, or as!. For example, use as? to conditionally downcast the first object in a heterogeneous array to a String as follows:
-->

인스턴스에 대해 구체적인 타입으로 `Any` 를 사용할 때 해당 프로퍼티 또는 메서드에 접근하려면 먼저 알려진 타입으로 인스턴스를 캐스팅 해야 합니다. `Any` 의 구체적인 타입인 인스턴스는 본래 동적 타입을 유지하고 `as`, `as?`, 또는 `as!` 와 같은 타입 캐스팅 연산자 (type-cast operators) 중 하나를 사용하여 타입을 캐스팅 할 수 있습니다. 예를 들어 `as?` 을 사용하여 배열의 첫번째 객체를 `String` 으로 조건부로 다운캐스트 합니다:

```swift
if let first = mixed.first as? String {
    print("The first item, '\(first)', is a string.")
}
// Prints "The first item, 'one', is a string."
```

<!--
For more information about casting, see Type Casting.

The AnyObject protocol is similar to the Any type. All classes implicitly conform to AnyObject. Unlike Any, which is defined by the language, AnyObject is defined by the Swift standard library. For more information, see Class-Only Protocols and AnyObject.
-->

캐스팅에 대한 자세한 내용은 [타입 캐스팅 (Type Casting)](../language-guide-1/type-casting.md) 을 참고 바랍니다.

`AnyObject` 프로토콜은 `Any` 타입과 유사합니다. 모든 클래스는 암시적으로 `AnyObject` 를 준수합니다. 언어에 의해 정의되는 `Any` 와 달리 `AnyObject` 는 Swift 표준 라이브러리에 의해 정의됩니다. 더 자세한 내용은 [클래스 전용 프로토콜 (Class-Only Protocols)](../language-guide-1/protocols.md#class-only-protocols) 와 [`AnyObject`](https://developer.apple.com/documentation/swift/anyobject) 를 참고 바랍니다.

> GRAMMAR OF AN ANY TYPE\
> any-type → `Any`

## Self 타입 (Self Type)

<!--
The Self type isn’t a specific type, but rather lets you conveniently refer to the current type without repeating or knowing that type’s name.

In a protocol declaration or a protocol member declaration, the Self type refers to the eventual type that conforms to the protocol.

In a structure, class, or enumeration declaration, the Self type refers to the type introduced by the declaration. Inside the declaration for a member of a type, the Self type refers to that type. In the members of a class declaration, Self can appear only as follows:

* As the return type of a method
* As the return type of a read-only subscript
* As the type of a read-only computed property
* In the body of a method

For example, the code below shows an instance method f whose return type is Self.
-->

`Self` 타입은 특정 타입이 아니라 해당 타입의 이름을 반복하거나 알지 않아도 현재 타입을 편리하게 참조할 수 있습니다.

프로토콜 선언 또는 프로토콜 멤버 선언에서 `Self` 타입은 프로토콜을 준수하는 최종 타입을 나타냅니다.

구조체, 클래스, 또는 열거형 선언에서 `Self` 타입은 선언에 의해 도입된 타입을 참조합니다. 타입의 멤버에 대한 선언 내에서 `Self` 타입은 해당 타입을 참조합니다. 클래스 선언의 멤버에서 `Self` 는 다음을 나타낼 수 있습니다:

* 메서드의 반환 타입
* 읽기전용 서브 스크립트의 반환 타입
* 읽기전용 계산된 프로퍼티의 타입
* 메서드의 바디

예를 들어 아래의 코드는 반환 타입이 `Self` 인 인스턴스 메서드 `f` 를 보여줍니다.

For example, the code below shows an instance method `f` whose return type is `Self`.

```swift
class Superclass {
    func f() -> Self { return self }
}
let x = Superclass()
print(type(of: x.f()))
// Prints "Superclass"

class Subclass: Superclass { }
let y = Subclass()
print(type(of: y.f()))
// Prints "Subclass"

let z: Superclass = Subclass()
print(type(of: z.f()))
// Prints "Subclass"
```

<!--
The last part of the example above shows that Self refers to the runtime type Subclass of the value of z, not the compile-time type Superclass of the variable itself.

Inside a nested type declaration, the Self type refers to the type introduced by the innermost type declaration.

The Self type refers to the same type as the type(of:) function in the Swift standard library. Writing Self.someStaticMember to access a member of the current type is the same as writing type(of: self).someStaticMember.
-->

위의 예제의 마지막 부분은 `Self` 가 변수 자체의 컴파일 타임 타입 (compile-time type) `Superclass` 가 아닌 `z` 값의 런타임 타입 (runtime type) `Subclass` 를 참조하는 것을 보여줍니다.

중첩된 타입 선언 내에서 `Self` 타입은 가장 안쪽 타입 선언에 의해 도입된 타입을 참조합니다.

`Self` 타입은 Swift 표준 라이브러리에서 [`type(of:)`](https://developer.apple.com/documentation/swift/2885064-type) 함수와 동일한 타입을 참조합니다. 현재 타입의 멤버를 접근하기 위해 `Self.someStaticMember` 라고 작성하는 것은 `type(of:self).someStaticMember` 로 작성하는 것과 동일합니다.

> GRAMMAR OF A SELF TYPE\
> self-type → `Self`

## 타입 상속 절 (Type Inheritance Clause)

<!--
A type inheritance clause is used to specify which class a named type inherits from and which protocols a named type conforms to. A type inheritance clause begins with a colon (:), followed by a list of type identifiers.

Class types can inherit from a single superclass and conform to any number of protocols. When defining a class, the name of the superclass must appear first in the list of type identifiers, followed by any number of protocols the class must conform to. If the class doesn’t inherit from another class, the list can begin with a protocol instead. For an extended discussion and several examples of class inheritance, see Inheritance.

Other named types can only inherit from or conform to a list of protocols. Protocol types can inherit from any number of other protocols. When a protocol type inherits from other protocols, the set of requirements from those other protocols are aggregated together, and any type that inherits from the current protocol must conform to all of those requirements.

A type inheritance clause in an enumeration definition can be either a list of protocols, or in the case of an enumeration that assigns raw values to its cases, a single, named type that specifies the type of those raw values. For an example of an enumeration definition that uses a type inheritance clause to specify the type of its raw values, see Raw Values.
-->

_타입 상속 절 (type inheritance clause)_ 은 명명된 타입이 상속하는 클래스와 명명된 타입이 준수하는 프로토콜을 지정하기 위해 사용됩니다. 타입 상속 절은 콜론 (`:`) 으로 시작하고 그 뒤에 타입 식별자의 목록이 옵니다.

클래스 타입은 단일 상위 클래스를 상속할 수 있고 여러개의 프로토콜을 준수할 수 있습니다. 클래스를 정의할 때 상위 클래스의 이름은 타입 식별자의 목록에서 첫번째로 나타나야 하고 다음으로 준수하는 여러개의 프로토콜이 옵니다. 클래스가 다른 클래스를 상속하지 않으면 목록은 대신 프로토콜로 시작할 수 있습니다. 클래스 상속에 대한 자세한 설명과 예제는 [상속 (Inheritance)](../language-guide-1/inheritance.md) 를 참고 바랍니다.

다른 명명된 타입은 프로토콜의 목록에서 상속하거나 준수할 수 있습니다. 프로토콜 타입은 여러 다른 프로토콜을 상속할 수 있습니다. 프로토콜 타입은 다른 프로토콜을 상속할 때 다른 프로토콜의 요구사항을 모으고 현재 프로토콜에서 상속되는 모든 타입은 모든 요구사항을 준수해야 합니다.

열거형 정의에 타입 상속 절은 프로토콜의 목록이거나 케이스에 원시값 (raw values) 을 할당하는 열거형인 경우 해당 원시값의 타입을 지정하는 단일 명명된 타입일 수 있습니다. 타입 상속 절을 사용하여 원시값의 타입을 지정하는 열거형 정의의 예는 [원시값 (Raw Values)](../language-guide-1/enumerations.md#raw-values) 를 참고 바랍니다.

> GRAMMAR OF A TYPE INHERITANCE CLAUSE\
> type-inheritance-clause → `:` [type-inheritance-list](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-inheritance-list)\
> type-inheritance-list → [attributes](attributes.md#unknown) $$_{opt}$$ [type-identifier](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-identifier) | [attributes](attributes.md#unknown) $$_{opt}$$ [type-identifier](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-identifier) `,` [type-inheritance-list](https://docs.swift.org/swift-book/ReferenceManual/Types.html#grammar\_type-inheritance-list)

## 타입 추론 (Type Inference)

<!--
Swift uses type inference extensively, allowing you to omit the type or part of the type of many variables and expressions in your code. For example, instead of writing var x: Int = 0, you can write var x = 0, omitting the type completely—the compiler correctly infers that x names a value of type Int. Similarly, you can omit part of a type when the full type can be inferred from context. For example, if you write let dict: Dictionary = ["A": 1], the compiler infers that dict has the type Dictionary<String, Int>.

In both of the examples above, the type information is passed up from the leaves of the expression tree to its root. That is, the type of x in var x: Int = 0 is inferred by first checking the type of 0 and then passing this type information up to the root (the variable x).

In Swift, type information can also flow in the opposite direction—from the root down to the leaves. In the following example, for instance, the explicit type annotation (: Float) on the constant eFloat causes the numeric literal 2.71828 to have an inferred type of Float instead of Double.
-->

Swift 는 광범위하게 _타입 추론 (type inference)_ 를 사용하므로 코드에서 많은 변수와 표현식의 타입 또는 타입의 부분을 생략할 수 있습니다. 예를 들어 `var x: Int = 0` 으로 작성하는 대신에 `var x = 0` 으로 타입을 완벽하게 생략하고 작성할 수 있습니다—컴파일러는 `x` 를 타입 `Int` 의 값으로 추론합니다. 유사하게 컨텍스트에서 전체 타입이 추론될 수 있을 때 타입의 부분을 생략할 수 있습니다. 예를 들어 `let dict: Dictionary = ["A": 1]` 을 작성하면 컴파일러는 `dict` 이 타입 `Dictionary<String, Int>` 이라고 추론합니다.

위의 두 예제에서 타입 정보는 표현식 트리의 잎에서 루트까지 전달됩니다. 즉, `var x: Int = 0` 에서 `x` 의 타입은 먼저 `0` 의 타입을 확인한 다음에 이 타입 정보를 루트 (변수 `x`) 까지 전달하여 유추합니.

Swift 에서 타입 정보는 루트에서 잎까지 반대로 흐를 수도 있습니다. 예를 들어 다음 예제에서 상수 `eFloat` 에 명시적 타입 주석 (`: Float`) 은 숫자 리터럴 `2.71828` 이 `Double` 이 아닌 `Float` 타입을 유추하도록 합니다.

```swift
let e = 2.71828 // The type of e is inferred to be Double.
let eFloat: Float = 2.71828 // The type of eFloat is Float.
```

<!--
Type inference in Swift operates at the level of a single expression or statement. This means that all of the information needed to infer an omitted type or part of a type in an expression must be accessible from type-checking the expression or one of its subexpressions.
-->

Swift 에서 타입 추론은 단일 표현식 또는 구문 수준에서 동작합니다. 이것은 표현식에서 생략된 타입 또는 타입의 일부를 유추하는데 필요한 모든 정보는 표현식 또는 하위 표현식 중 하나를 타입 검사 (type-checking) 하여 접근할 수 있습니다.
