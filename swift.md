Various Notes on the Swift Programming Language from Documentation

## The Swift Programming Language Documentation

#### The Basics

##### Constants and Variables

**Declaring Constants and Variables**
- associate a name with a value of a particular type
- value of a constant can't be changed once set, whereas variable can be set to different value in future
- declare constant with `let`
```
let maximumNumberOfLoginAttempts = 10
```
- declare variable with `var`
```
var currentLoginAttempt = 0
```
- can declare multiple constants or multiple variables on a single line separated by commas
```
var x = 0.0, y = 0.0, z = 0.0
```

**Type Annotations**
- you can provide a type annotation when you declare a constant or variable, to be clear about the kind of values the let/var can store
```
var welcomeMessage: String
welcomeMessage = "Hello"
```
- can define multiple variables of same type on single line separated by commas
```
var red, green, blue: Double
```

**Naming Constants and Varialbes**
- names can contain almost any character, including unicode
- names can't contain whitespace, math symbols, arrows, line/box character
- names can't begin with a number

**Printing Constants and Variables**
- can print the current value of a constant or variable with print function
```
print(welcomeMessage)
// Prints "Hello"
```
- swift can print using string interpolation
```
print("The current value of welcomeMessage is \(welcomeMessage)")
// Prints "The current value of welcomeMessage is Hello"
```

##### Comments

```
// This is a comment.

/* This is also a comment
but is written over multiple lines. */
```

##### Semicolons

- semicolons are not required after each statement unelss you want to write multiple separate statements on a single line
```
let cat = "catEmoji"; print(cat)
// Prints "catEmoji"
```

##### Integers

- whole numbers without a fractional component

**Integer Bounds**
- can access min and max values of each integer type with min and max properties
```
let minValue = UInt8.min // minValue is equal to 0, and is of type UInt8
let maxValue = UInt8.max // maxValue is equal to 255, and is of type UInt8
```

**Int**
- unless you need to work with a specific size of integer, always use Int values in your code
  - on a 32 bit platform, Int is the same size as Int32
  - on a 64 bit platform, Int is the same size as Int64

**UInt**
- an unsigned integer type

##### Floating-Point numbers

- numbers with a fractional component such as 3.14159, 0.1, and -27.31
- can represent wider range than values of integer types and can store numbers that are larger or smaller than can be stored in an Int
- two signed floating-point number types
  - Double represents a 64 bit floating-point number
  - Float represents a 32 bit floating-point number

##### Type Safety and Type Inference

- Swift is a type-safe language; it encourages you to be clear about the types of values your code can work with
- Swift performs type checks when compiling your code and flags any mismatched types as errors
- if you don't specify the type of value you need, Swift uses type inference to work out the appropriate type
```
let meaningOfLife = 42
// meaningOfLife is inferred to be of type Int

let pi = 3.14159
// pi is inferred to be of type Double, Swift always chooses Double over Float when inferring floating point numbers
```

##### Numeric Literals

- integer literals can be written as
```
let decimalInteger = 17
let binaryInteger = 0b10001 // 17 in binary notation
let octalInteger = 0o21 // 17 in octal notation
let hexadecimalInteger = 0x11 // 17 in hexadecimal notation
```

##### Numeric Type Conversion

**Integer Conversion**
- use the Int type for all general-purpose integer constants and variables in your code
- range of numbers that can be stored in integer let/var is different for each numeric type
```
let cannotBeNegative: UInt8 = -1
// UInt8 cannot store negative numbers, and so this will report an error
let tooBig: Int8 = Int8.max + 1
// Int8 cannot store a number larger than its maximum value,
// and so this will also report an error
```

- to convert oen specific type to another, initialize a new number of desired type with the existing value
```
// can't be added directly because not of same type, so have to convert both to UInt16...
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```

**Integer and Floating-Point Conversion**
- conversions between integer and floating-point must be made explicit
```
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi equals 3.14159, and is inferred to be of type Double
```
- integer type can be initialized with a Double or Float value
```
let integerPi = Int(pi)
// integerPi equals 3, and is inferred to be of type Int
// floating point values are always truncated, so 4.75 becomes 4 and -3.9 becomes -3
```

##### Booleans
- boolean type is Bool, of constant values true or false

##### Tuples
- group multiple values into a single compound value
- can be of any type and don't have to match
- useful as return values of functions
```
let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")
// a tuple of type (int, String)
```
- you can name the individual elements in a tuple when it is defined
```
let http200Status = (statusCode: 200, description: "OK")
print("The status code is \(http200Status.statusCode)")
// Prints "The status code is 200"
print("The status message is \(http200Status.description)")
// Prints "The status message is OK"
```

##### Optionals
- use optionals in situations where a value may be absent, it represents two possibilities
  - either there **is** a value and you can unwrap the optional to access that value
  - or there isn't a value at all

```
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// convertedNumber is inferred to be of type "Int?", or "optional Int"
```

The question mark above indicates that the value it contains is optional, it might contain some Int value, or it might contain no value at all (and it can't contain anything else, like a bool or a string)

- you set an optional variable to a valueless state by assigning it the special value nil
- if a constant/variable in your code needs to work with the absence of a value under certain conditions, always declare it as an optional value of the appropriate type
```
var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value
```

**Nil**
- if you define an optional variable without providing a default value, the variable is auto set to nil
```
var surveyAnswer: String?
// surveyAnswer is automatically set to nil
```

**If Statements and Forced Unwrapping**

If an optional has a value it is considered 'not equal to' nil...
```
if convertedNumber != nil {
    print("convertedNumber contains some integer value.")
}
// Prints "convertedNumber contains some integer value."
```
Once you're sure the optional does have a value, you can access using ! at the end of optional's name
  - "I know this optional definitely has a value, please use it" known as forced unwrapping
```
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber!).")
}
// Prints "convertedNumber has an integer value of 123."
```

**Optional Binding**

Use optional binding to find out if optional has value, if so, make that value available as a temporary constant or variable.
- constants and variables created with optional binding in if statement are only available within body of if statement

Above example can be rewritten as...
```
if let actualNumber = Int(possibleNumber) {
    print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("The string \"\(possibleNumber)\" could not be converted to an integer")
}
// Prints "The string "123" has an integer value of 123"
```
- “If the optional Int returned by Int(possibleNumber) contains a value, set a new constant called actualNumber to the value contained in the optional."

**Implicitly Unwrapped Optionals**

Sometimes it's clear that an optional will always have a value after the first value is set. In such cases, it's useful to remove the need to check and unwrap the optional's value every time it's accessed because it can be assumed to have a value all of the time. This is an example of implicitly unwrapped optional.

- written as `String!` instead of `String?`
- primary use is during class initialization

Example of optional string and implicitly unwrapped optional string when accessing their value as an explicit string...

```
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // requires an exclamation mark

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // no need for an exclamation mark
```

Can think of implicitly wrapped optional as giving permission for the optional to be unwrapped automatically whenever it's used.

#####Error Handling

```
func makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
```

In this example, makeASandwich() function will throw an error if no clean dishes are available or if any ingredients are missing. Because makeASandwich() can throw an error, the function call is wrapped in a try expression. By wrapping the function call in a do statement, any errors that are thrown will be propagated to the provided catch clauses.

#####Assertions and Preconditions

- Assertions and preconditions are checks that happen at runtime
- assertions are checked only in debug builds, in production builds the condition inside an assertion is not evaluated
- preconditions are checked in both debug and production builds

**Debugging with Assertions**

```
let age = -3
assert(age >= 0, "A person's age can't be less than zero.")
// This assertion fails because -3 is not >= 0.
```

Or if the code already checks the condition you can use...

```
if age > 10 {
    print("You can ride the roller-coaster or the ferris wheel.")
} else if age >= 0 {
    print("You can ride the ferris wheel.")
} else {
    assertionFailure("A person's age can't be less than zero.")
}
```

**Enforcing Preconditions**

Use precondition when a condition has the chance to be false, but must definitely be true for code to continue.

```
// In the implementation of a subscript...
precondition(index > 0, "Index must be greater than zero.")
```

####Basic Operators

#####Terminology

Unary - operators on a single target such as `-a`, `!b`, `c!`
Binary - operators on two targets such as `2 + 3`
Ternary - operators on three targets `a ? b : c`

#####Assignment Operator

```
let b = 10
var a = 5
a = b
// a is now equal to 10

let (x, y) = (1, 2)
// x is equal to 1, and y is equal to 2
```

#####Arithmetic Operators

```
1 + 2       // equals 3 - addition
5 - 3       // equals 2 - subtraction
2 * 3       // equals 6 - multiplication
10.0 / 2.5  // equals 4.0 - division
```

String Concatenation

```
"hello, " + "world"  // equals "hello, world"
```

#####Remainder Operator

```
9 % 4    // equals 1
-9 % 4   // equals -1
```

- the sign of b is ignored so `a % b` and `a % -b` is always the same

#####Comparison Operators

```
1 == 1   // true because 1 is equal to 1
2 != 1   // true because 2 is not equal to 1
2 > 1    // true because 2 is greater than 1
1 < 2    // true because 1 is less than 2
1 >= 1   // true because 1 is greater than or equal to 1
2 <= 1   // false because 2 is not less than or equal to 1
```

```
let name = "world"
if name == "world" {
    print("hello, world")
} else {
    print("I'm sorry \(name), but I don't recognize you")
}
// Prints "hello, world", because name is indeed equal to "world".
```

```
(1, "zebra") < (2, "apple")   // true because 1 is less than 2; "zebra" and "apple" are not compared
(3, "apple") < (3, "bird")    // true because 3 is equal to 3, and "apple" is less than "bird"
(4, "dog") == (4, "dog")      // true because 4 is equal to 4, and "dog" is equal to "dog"
```

- Because 1 is less than 2, (1, "zebra") is considered less than (2, "apple"), regardless of any other values in the tuples. It doesn’t matter that "zebra" isn’t less than "apple", because the comparison is already determined by the tuples’ first elements

#####Nil-Coalescing Operator

`a??b` unwraps an optional `a` if it contains a value, or returns a default value `b` if `a` is nil

It is shorthand for the code below...

```
a != nil ? a! : b
```

The nil-coalescing operator uses ternary conditional operator and forced unwrapping to access the value wrapped inside `a` when `a` is not nil, and returns `b` otherwise.

```
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil

var colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName is nil, so colorNameToUse is set to the default of "red"
```

#####Range Operators

Closed Range Operator
`a...b` defines a range that runs form `a` to `b` and includes both values

Half Open Range Operator
`a..<b` defines a range that runs from `a` to `b`, but doesn't include `b`

One Sided Ranges
- for ranges that continue as far as possible in one direction

```
for name in names[2...] {
    print(name)
}
// Brian
// Jack

for name in names[...2] {
    print(name)
}
// Anna
// Alex
// Brian
```

####Strings and Characters

#####String Literals

`let someString = "Some string literal value"`

**Multiline String Literals**

```
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

- if you want to make the code easier to read, can use `\`

```
let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin, \
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on \
till you come to the end; then stop."
"""
```

```
let lineBreaks = """

This string starts with a line break.
It also ends with a line break.

"""
```

- Spaces are ignored up until the closing `"""`

```
let linesWithIndentation = """
    This line doesn't begin with whitespace.
        This line begins with four spaces.
    This line doesn't begin with whitespace.
    """
```

**Special Characters in String Literals**

`\0` - null character
`\\` - backslash
`\t` - horizontal tab
`\n` - line feed
`\r` - carriage return
`\"` - double quote
`\'` - single quote
`\u{n}` - unicode scalar value where n is 1-8 digit hexadecimal number

```
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496
```

#####Initializing an Empty String

```
var emptyString = ""               // empty string literal
var anotherEmptyString = String()  // initializer syntax
// these two strings are both empty, and are equivalent to each other
```

#####String Mutability

```
var variableString = "Horse"
variableString += " and carriage"
// variableString is now "Horse and carriage"

let constantString = "Highlander"
constantString += " and another Highlander"
// this reports a compile-time error - a constant string cannot be modified
```

#####Strings are Value Types

If you create a new String value, that value is copied when it's passed to a function, method, or when it's assigned to a constant/variable.

This ensures that when a function/method passes you a String value, it's clear that you own that exact String value - regardless of where it came from.

#####Working with Characters

Can access individual Character values for a String by iterating over...

```
for character in "Dog!🐶" {
    print(character)
}
// D
// o
// g
// !
// 🐶
```

String values can be constructed by passing array of Character values as arg to initializer...

```
let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// Prints "Cat!🐱"
```

#####String Interpolation

```
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message is "3 times 2.5 is 7.5"
```

#####Unicode

```
let eAcute: Character = "\u{E9}"                         // é
let combinedEAcute: Character = "\u{65}\u{301}"          // e followed by ́
// eAcute is é, combinedEAcute is é

let precomposed: Character = "\u{D55C}"                  // 한
let decomposed: Character = "\u{1112}\u{1161}\u{11AB}"   // ᄒ, ᅡ, ᆫ
// precomposed is 한, decomposed is 한
```

#####Counting Characters

```
let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
print("unusualMenagerie has \(unusualMenagerie.count) characters")
// Prints "unusualMenagerie has 40 characters"
```

```
var word = "cafe"
print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in cafe is 4"

word += "\u{301}"    // COMBINING ACUTE ACCENT, U+0301

print("the number of characters in \(word) is \(word.count)")
// Prints "the number of characters in café is 4"
```

#####Accessing and Modifying a String

**String Indices**

```
let greeting = "Guten Tag!"
greeting[greeting.startIndex]
// G
greeting[greeting.index(before: greeting.endIndex)]
// !
greeting[greeting.index(after: greeting.startIndex)]
// u
let index = greeting.index(greeting.startIndex, offsetBy: 7)
greeting[index]
// a
```

```
for index in greeting.indices {
    print("\(greeting[index]) ", terminator: "")
}
// Prints "G u t e n   T a g ! "
```

**Inserting and Removing**

Inserting
```
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome now equals "hello!"

welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there!"
```

Removing
```
welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there"

let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)
// welcome now equals "hello"
```

#####Substrings

Use substrings for only a short amount of time while performing actions on a string
```
let greeting = "Hello, world!"
let index = greeting.firstIndex(of: ",") ?? greeting.endIndex
let beginning = greeting[..<index]
// beginning is "Hello"

// Convert the result to a String for long-term storage.
let newString = String(beginning)
```

#####Comparing Strings

**String Character Equality**

- checked with teh `==` or `!=` operator

```
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```

```
// "Voulez-vous un café?" using LATIN SMALL LETTER E WITH ACUTE
let eAcuteQuestion = "Voulez-vous un caf\u{E9}?"

// "Voulez-vous un café?" using LATIN SMALL LETTER E and COMBINING ACUTE ACCENT
let combinedEAcuteQuestion = "Voulez-vous un caf\u{65}\u{301}?"

if eAcuteQuestion == combinedEAcuteQuestion {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```

**Prefix and Suffix Equality**

```
let romeoAndJuliet = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]

//can use hasPrefix(_:) method to count the number of scenes in Act 1 of the play

var act1SceneCount = 0
for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 1 ") {
        act1SceneCount += 1
    }
}
print("There are \(act1SceneCount) scenes in Act 1")
// Prints "There are 5 scenes in Act 1"

//similarly hasSuffix(_:) to count number of scenes that take place in or around Capulet's mansion and Friar Lawrence's cell

var mansionCount = 0
var cellCount = 0
for scene in romeoAndJuliet {
    if scene.hasSuffix("Capulet's mansion") {
        mansionCount += 1
    } else if scene.hasSuffix("Friar Lawrence's cell") {
        cellCount += 1
    }
}
print("\(mansionCount) mansion scenes; \(cellCount) cell scenes")
// Prints "6 mansion scenes; 2 cell scenes"
```

####Collection Types

Swift provides 3 primary collection types - arrays, sets, and dictionaries (key value pairs), for storing collections of values.

#####Mutability of Collections

- Arrays, sets and dictionaries set to variable are mutable (can be modified)
- Arrays, sets and dictionaries set to a constant are immutable (size and contents cannot be chagned)

#####Arrays

- Stores values of the same type in an ordered list
- The same value can appear multiple times at different positions

**Array Type Shorthand Syntax**

- the full syntax is `Array<Element>` where `Element` is the type of values the array is allowed to store
- the shorthand syntax is `[Element]`

**Creating an Empty Array**

```
var someInts = [Int]()
print("someInts is of type [Int] with \(someInts.count) items.")
// Prints "someInts is of type [Int] with 0 items."
```

**Creating an Array with a Default Value**

Swift has initializer to create array of certain size with all values set to default value...

```
var threeDoubles = Array(repeating: 0.0, count: 3)
// threeDoubles is of type [Double], and equals [0.0, 0.0, 0.0]
```

**Creating an Array by Adding Two Arrays Together**

```
var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
// anotherThreeDoubles is of type [Double], and equals [2.5, 2.5, 2.5]

var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles is inferred as [Double], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```

**Creating an Array with an Array Literal**

```
var shoppingList: [String] = ["Eggs", "Milk"]
// shoppingList has been initialized with two initial items
```

**Accessing and Modifying an Array**

Find out the number of items in array with `count` method...

```
print("The shopping list contains \(shoppingList.count) items.")
// Prints "The shopping list contains 2 items."
```

Boolean `isEmpty` method to check if `count` property is equal to 0...

```
if shoppingList.isEmpty {
    print("The shopping list is empty.")
} else {
    print("The shopping list is not empty.")
}
// Prints "The shopping list is not empty."
```

Add to end with `append` method...

```
shoppingList.append("Flour")
// shoppingList now contains 3 items, and someone is making pancakes
```

Append array of 1+ compatible items with += operator...

```
shoppingList += ["Baking Powder"]
// shoppingList now contains 4 items
shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
// shoppingList now contains 7 items
```

Retrieve a value with subscript syntax...

```
var firstItem = shoppingList[0]
// firstItem is equal to "Eggs"
```

Can also change a value at given index with subscript syntax...

```
shoppingList[0] = "Six eggs"
// the first item in the list is now equal to "Six eggs" rather than "Eggs"
```

Can use subscript syntax to change a range of values at once...

```
shoppingList[4...6] = ["Bananas", "Apples"]
// shoppingList now contains 6 items
// replaces Chocolate Spread, Cheese, and Butter with Bananas and Apples
```

To insert an item into array at specified index, call arrays insert at method...

```
shoppingList.insert("Maple Syrup", at: 0)
// shoppingList now contains 7 items
// "Maple Syrup" is now the first item in the list
```

Similarly remove an item with remove at method...

```
let mapleSyrup = shoppingList.remove(at: 0)
// the item that was at index 0 has just been removed
// shoppingList now contains 6 items, and no Maple Syrup
// the mapleSyrup constant is now equal to the removed "Maple Syrup" string
```

If you need to remove final item of array, use removeLast instead of remove at to avoid the need to query the count property...

```
let apples = shoppingList.removeLast()
// the last item in the array has just been removed
// shoppingList now contains 5 items, and no apples
// the apples constant is now equal to the removed "Apples" string
```

**Iterating Over an Array**

Can iterate over an entire array with for-in loop...

```
for item in shoppingList {
    print(item)
}
// Six eggs
// Milk
// Flour
// Baking Powder
// Bananas
```

If you need index as well as value, use enumerated method...

- enumerated returns a tuple composed of an integer and an item

```
for (index, value) in shoppingList.enumerated() {
  print("Item \(index + 1"): \(value)")
}
// Item 1: Six eggs
// Item 2: Milk
// Item 3: Flour
// Item 4: Baking Powder
// Item 5: Bananas
```

#####Sets

Set stores distinct values of the same type in a collection with no defined ordering. You can use a set instead of an array when order of items is not important, or if you need to ensure an item only appears once.

**Hash Values for Set Types**

- type must be hashable in order to be stored in a set
  - a hash value is an Int value that is same for all objects that compare equally such that if a == b, a.hashValue == b.hashValue
- all of Swift's basic types (string, Int, Double, Bool) are hashable

**Set Type Syntax**

- type of a Swift set is written as `Set<Element>` where Element is the type that set is allowed to store

**Creating and Initializing an Empty Set**

```
var letters = Set<Character>()
print("letters is of type Set<Character> with \ (letters.count) items.")
// Prints "letters is of type Set<Character> with 0 items."
```

If context provides type of information such as function argument or variable/constant, you can create an empty set with an empty array literal...

```
letters.insert("a")
// letters now contains 1 value of type Character
letters = []
// letters is now an empty set, but is still of type Set<character>
```

**Creating a Set with an Array Literal**

Can also initialize a set with array literal, as shorthand way to write one or more values as a set collection.

Ex. set called favoriteGenres to store String values...

```
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
// favoriteGenres has been initialized with three initial items
```

OR written with type inference as...

```
var favoriteGenres: Set = ["Rock", "Classical", "Hip Hop"]
```

**Accessing and Modifying a Set**

Access/modify a set through its methods and properties

To find number of items in a set, check its read-only count property...

```
print("I have \(favoriteGenres.count) favorite music genres.")
// Prints "I have 3 favorite music genres."
```

Use Boolean isEmpty property as shortcut for checking if count property is 0...

```
if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky.")
} else {
    print("I have particular music preferences.")
}
// Prints "I have particular music preferences."
```

Can add a new item into a set by calling insert method...

```
favoriteGenres.insert("Jazz")
// favoriteGenres now contains 4 items
```

Can remove an item by calling remove method...

- removes item and returns the value, or returns nil if set did not contain it
- all items can be removed with removeAll() method

```
if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre)? I'm over it.")
} else {
    print("I never much cared for that.")
}
// Prints "Rock? I'm over it."
```

Use contains() method to check for particular item...

```
if favoriteGenres.contains("Funk") {
    print("I get up on the good foot.")
} else {
    print("It's too funky in here.")
}
// Prints "It's too funky in here."
```

**Iterating Over a Set**

Can iterate over values with for-in loop...

```
for genre in favoriteGenres {
    print("\(genre)")
}
// Classical
// Jazz
// Hip hop
```

Since there is not defined ordering, can use sorted() method to return elements as an array sorted using the < operator

```
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}
// Classical
// Hip hop
// Jazz
```


#####Performing Set Operations

**Fundamental Set Operations**

- use intersection method to create a new set with only the values common in both sets
- use symmetricDifference method to create a new set witih values in either set, but not both
- use union method to create a new set with all of the values in both sets
- use subtracting method to create a new set with values not in the specified set

```
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]

oddDigits.union(evenDigits).sorted()
// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
oddDigits.intersection(evenDigits).sorted()
// []
oddDigits.subtracting(singleDigitPrimeNumbers).sorted()
// [1, 9]
oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()
// [1, 2, 9]
```

**Set Membership and Equality**

- use the is equal operator (==) to determine whether two sets contain all same values
- use isSubset(of:) method to determine if all values of a set are contained in specified set
- use isSuperset(of:) method to determine whether a set contains all of the values in a specified set
- use isStrictSubset(of:) or isStrictSuperset(of:) methods to determine if a set is a subset or a superset, but not equal to, a specified set
- use isDisjoin(with:) method to determine if two sets have no values in common

```
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]

houseAnimals.isSubset(of: farmAnimals)
// true
farmAnimals.isSuperset(of: houseAnimals)
// true
farmAnimals.isDisjoint(with: cityAnimals)
// true
```

#####Dictionaries

- items have no specified order
- each value is associated with a unique key, which acts as an identifier for value within the dictionary

**Dictionary Type Shorthand Syntax**

Type of Swift dictionary is written in full as `Dictionary<Key, Value>` where key is the type of value that can be used as dictionary key, and value is the type of value that the dictionary stores for those keys

- can also write in shorthand form as `[Key: Value]`

**Creating an Empty Dictionary**

As with arrays, can create empty Dictionary using initializer syntax...

```
var namesOfIntegers = [Int: String]()
// namesOfIntegers is an empty [Int: String] dictionary
```

Above example creates empty dictionary of type [Int: String] to store human-readable names of integer values

If context already provided type information, can create an empty dictionary with `[:]`...

```
namesOfIntegers[16] = "sixteen"
// namesOfIntegers now contains 1 key-value pair
namesOfIntegers = [:]
// namesOfIntegers is once again an empty dictionary of type [Int: String]
```

**Creating a Dictionary with a Dictionary Literal**

```
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```

or without the types, because literal is obvious of type

```
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```

**Accessing and Modifying a Dictionary**

Access and modify a dictionary through its methods and properties, or by using subscript syntax...

Find number of items in Dictionary by checking its read-only count property...

```
print("The airports dictionary contains \(airports.count) items.")
// Prints "The airports dictionary contains 2 items."
```

Use the Boolean isEmpty property as a shortcut for checking whether the count property is equal to 0...

```
if airports.isEmpty {
    print("The airports dictionary is empty.")
} else {
    print("The airports dictionary is not empty.")
}
// Prints "The airports dictionary is not empty."
```

Can add new item to dictionary with subscript syntax...

```
airports["LHR"] = "London"
// the airports dictionary now contains 3 items
```

Can also use subscript syntax to change value associated with a particular key...

```
airports["LHR"] = "London Heathrow"
// the value for "LHR" has been changed to "London Heathrow"
```

Alternate to subscripting, use a dictionary's updateValue method to set/update value for particular key, this method returns the old value after performing an update

The updateValue method returns an optional value of the dictionary's value type, the optional value contains the old value for that key if one existed before the update, or nil if no value existed.

```
if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
    print("The old value for DUB was \(oldValue).")
}
// Prints "The old value for DUB was Dublin."
```

You can use subscript syntax to retrieve a value form the dictionary for a particular key. Because it's possible to request a key for which no value exists, a dictionary's subscript returns an optional value of the dictionary's value type. If the dictionary contains a value for the requested key, the subscript returns an optional value for the requested key, otherwise returns nil.

```
if let airportName = airports["DUB"] {
    print("The name of the airport is \(airportName).")
} else {
    print("That airport is not in the airports dictionary.")
}
// Prints "The name of the airport is Dublin Airport."
```

Can use subscript syntax to remove a key-value pair from dictionary by assigning nil for value of that key

```
airports["APL"] = "Apple International"
// "Apple International" is not the real airport for APL, so delete it
airports["APL"] = nil
// APL has now been removed from the dictionary
```

Alternatively, remove a key-value pair from a dictionary with the removeValue(forKey:) method. This method removes the key-value pair if it exists and returns the removed value, or returns nil if no value existed:

```
if let removedValue = airports.removeValue(forKey: "DUB") {
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary does not contain a value for DUB.")
}
// Prints "The removed airport's name is Dublin Airport."
```

**Iterating Over a Dictionary**

Can iterate over key-value pairs with a for-in loop, each item is returned as a (key, value) tuple...

```
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
// YYZ: Toronto Pearson
// LHR: London Heathrow
```

Can also retrieve an iterable collection of a dictionary's keys or values by accessing its keys and values properties...

```
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: YYZ
// Airport code: LHR

for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: Toronto Pearson
// Airport name: London Heathrow
```

If you need to use a dictionary's keys or values with an API that takes an Array instance, initialize a new array with the keys or values property...

```
let airportCodes = [String](airports.keys)
// airportCodes is ["YYZ", "LHR"]

let airportNames = [String](airports.values)
// airportNames is ["Toronto Pearson", "London Heathrow"]
```

####Control Flow

#####For-In Loops

Use to iterate over a sequence, such as items in an array, ranges of numbers, or characters in a string...

```
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack!
```

Decompose dictionary key-value pairs into named constants...

```
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
// ants have 6 legs
// cats have 4 legs
// spiders have 8 legs
```

Numeric ranges...

```
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```

If you don't need each value from a sequence, can ignore the values by using an underscore in place of a variable name...

```
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")
// Prints "3 to the power of 10 is 59049"
```

Using half-open range operator...

```
let minutes = 60
for tickMark in 0..<minutes {
    // render the tick mark each minute (60 times)
}
```

Might want fewer ticks in UI, example one every 5 minutes. Use the stride(from:to:by:) function to skip unwanted marks...

```
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
}
```

Closed ranges are also available by using stride(from:through:by:) instead...

```
let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // render the tick mark every 3 hours (3, 6, 9, 12)
}
```

#####While Loops

Performs a set of statements until a condition becomes false

**While**

Evaluates its condition at the start of each pass through the loop

while condition {
  statements
}

Chutes and ladders example...

```
var square = 0
var diceRoll = 0
while square < finalSquare {
    // roll the dice
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
    if square < board.count {
        // if we're still on the board, move up or down for a snake or a ladder
        square += board[square]
    }
}
print("Game over!")
```

**Repeat While**

Evaluates its condition at the end of each pass through the loop

repeat {
  statements
} while condition

Chutes and ladders example...

```
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0

repeat {
    // move up or down for a snake or ladder
    square += board[square]
    // roll the dice
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
} while square < finalSquare
print("Game over!")
```

#####Conditional Statements

**If**

Final else clause is optional

```
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}
// Prints "It's really warm. Don't forget to wear sunscreen."
```

**Switch**

In its simplest form, a switch statement compares a value against one or more values of the same type...

```
PSEUDO CODE

switch some value to consider {
case value 1:
    respond to value 1
case value 2,
     value 3:
    respond to value 2 or 3
default:
    otherwise, do something else
}
```

```
let someCharacter: Character = "z"
switch someCharacter {
case "a":
    print("The first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}
// Prints "The last letter of the alphabet"
```

**No Implicit Fallthrough**

Switch statements in Swift do not fall through the bottom of each case and into the next one by default. Instead, the entire switch statement finishes its execution as soon as the first matching switch case is completed, without requiring an explicit break statement.

to make a switch with a single case that matches both "a" and "A", combine two values into a compound case, separating values with commas...

```
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a", "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// Prints "The letter A"
```

**Interval Matching**

Values in switch cases can be checked for their inclusion in an interval - example uses number intervals to provide a natural language count for numbers of any siez...

```
let approximateCount = 62
let countedThings = "moons orbiting Saturn"
let naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print("There are \(naturalCount) \(countedThings).")
// Prints "There are dozens of moons orbiting Saturn."
```

**Tuples**

**Value Bindings**

**Where**

**Compound Cases**

Multiple switch cases that share the same body can be combined by writing several patterns after case, with a comma between each of the patterns. If any of the patterns match, then the case is considered to match. The patterns can be written over multiple lines if the list is long...

```
let someCharacter: Character = "e"
switch someCharacter {
case "a", "e", "i", "o", "u":
    print("\(someCharacter) is a vowel")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
     "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    print("\(someCharacter) is a consonant")
default:
    print("\(someCharacter) is not a vowel or a consonant")
}
// Prints "e is a vowel"
```

Compound cases can also include value bindings...

```
let stillAnotherPoint = (9, 0)
switch stillAnotherPoint {
case (let distance, 0), (0, let distance):
    print("On an axis, \(distance) from the origin")
default:
    print("Not on an axis")
}
// Prints "On an axis, 9 from the origin"
```

#####Control Transfer Statements

Change the order in which your code is executed, by transferring control from one piece of code to another...

- continue
- break
- fallthrough
- return
- throw

**Continue**

**Break**

- ends execution of an entire control flow statement immediately  
- when used in a loop statement, break ends the loop's execution immediately and transfers control to the code after the loop's closing brace
- when used inside a switch statement, break causes the switch statement to end its execution immediately and to transfer control to the code after the switch statement's closing brace

```
let numberSymbol: Character = "三"  // Chinese symbol for the number 3
var possibleIntegerValue: Int?
switch numberSymbol {
case "1", "١", "一", "๑":
    possibleIntegerValue = 1
case "2", "٢", "二", "๒":
    possibleIntegerValue = 2
case "3", "٣", "三", "๓":
    possibleIntegerValue = 3
case "4", "٤", "四", "๔":
    possibleIntegerValue = 4
default:
    break
}
if let integerValue = possibleIntegerValue {
    print("The integer value of \(numberSymbol) is \(integerValue).")
} else {
    print("An integer value could not be found for \(numberSymbol).")
}
// Prints "The integer value of 三 is 3."
```

**Fallthrough**

Switch statements don't fall through the bottom of each case and into the next one. That is, the entire switch statement completes its execution as soon as the first matching case is completed. If you need fallthrough behavior, you can opt in to this behavior on a case-by-case basis with the fallthrough keyword.

```
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
default:
    description += " an integer."
}
print(description)
// Prints "The number 5 is a prime number, and also an integer."
```

**Labeled Statements**

#####Early Exit

A guard statement, like an if statemnet, executes statements depending on the Boolean value of an expression. A condition must be true in order for the code after the guard statement to be executed...unlike an if statement, guard statement always has an else clause.

```
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        return
    }

    print("Hello \(name)!")

    guard let location = person["location"] else {
        print("I hope the weather is nice near you.")
        return
    }

    print("I hope the weather is nice in \(location).")
}

greet(person: ["name": "John"])
// Prints "Hello John!"
// Prints "I hope the weather is nice near you."
greet(person: ["name": "Jane", "location": "Cupertino"])
// Prints "Hello Jane!"
// Prints "I hope the weather is nice in Cupertino."
````

**Checking API Availabliity**

####Functions

#####Defining and Calling Functions

Ex. input parameter of a String value called person, and return type of String
```
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}

print(greet(person: "Anna"))
// Prints "Hello, Anna!"
print(greet(person: "Brian"))
// Prints "Hello, Brian!"
```

#####Function Parameters and Return Values

**Functions Without Parameters**

```
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())
// Prints "hello, world"
```

**Functions With Multiple Parameters**

```
func greet(person: String, alreadyGreeted: Bool) -> String {
    if alreadyGreeted {
        return greetAgain(person: person)
    } else {
        return greet(person: person)
    }
}
print(greet(person: "Tim", alreadyGreeted: true))
// Prints "Hello again, Tim!"
```

**Functions Without Return Values**

```
func greet(person: String) {
    print("Hello, \(person)!")
}
greet(person: "Dave")
// Prints "Hello, Dave!"
```

**Functions With Multiple Return Values**

```
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}

// Can access values with dot syntax...

let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")
// Prints "min is -6 and max is 109"
```

#####Function Argument Labels and Parameter Names


Each function has both an argument label and a parameter name. By default, parameters use their parameter name as their argument label.

All parameters have unique names, but it's possible for multiple parameters to have the same argument label, unique argument labels help make your code more readable.

```
func someFunction(firstParameterName: Int, secondParameterName: Int) {
    // In the function body, firstParameterName and secondParameterName
    // refer to the argument values for the first and second parameters.
}
someFunction(firstParameterName: 1, secondParameterName: 2)
```

**Specifying Argument Labels**

You write an argument label before the parameter name, separated by a space.

```
func someFunction(argumentLabel parameterName: Int) {
    // In the function body, parameterName refers to the argument value
    // for that parameter.
}
```

Argument labels can allow a function to be called in an expressive, sentence-like manner, while still providing a function body that is readable/clear in intent.

Variation of the greeting function...

```
func greet(person: String, from hometown: String) -> String {
    return "Hello \(person)!  Glad you could visit from \(hometown)."
}
print(greet(person: "Bill", from: "Cupertino"))
// Prints "Hello Bill!  Glad you could visit from Cupertino."
```

**Omitting Argument Labels**

If you don't want an argument label for a param, write an underscore instead of an explicit arg label for that param.

```
func someFunction(_ firstParameterName: Int, secondParameterName: Int) {
    // In the function body, firstParameterName and secondParameterName
    // refer to the argument values for the first and second parameters.
}
someFunction(1, secondParameterName: 2)
```

**Default Parameter Values**

Can define a default value for any param in a func by assigning a value to the param after that param's type. If a default value is defined, you can omit that param when calling the func.

```
func someFunction(parameterWithoutDefault: Int, parameterWithDefault: Int = 12) {
    // If you omit the second argument when calling this function, then
    // the value of parameterWithDefault is 12 inside the function body.
}
someFunction(parameterWithoutDefault: 3, parameterWithDefault: 6) // parameterWithDefault is 6
someFunction(parameterWithoutDefault: 4) // parameterWithDefault is 12
```

**Variadic Parameters**

**In-Out Parameters**

#####Function Types

#####Nested Functions

All of the aforementioned functions have been global functions. You can also define functions inside the bodies of other functions.

- An enclosing func can return one of its nested functions to allow the nested function to be used in another scope

```
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backward ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// moveNearerToZero now refers to the nested stepForward() function
while currentValue != 0 {
    print("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
print("zero!")
// -4...
// -3...
// -2...
// -1...
// zero!
```

####Closures

####Enumerations

####Classes and Structures

#####Comparing Classes and Structures

Structures and classes have many things in common, both can:

- define properties to store values
- define methods to provide funcitonality
- define subscripts to provide access to their values using subscript syntax
- define initializers to set up their initial state
- be extended to expand their functionality beyond a default implementation
- conform to protocols to provide standard functionality of a certain kind

Classes have additional capabilities that structures don't have:

- inheritance enables one class to inherit the characteristics of another
- type casting enables you to check and interpret the type of a class instance at runtime
- deinitializers enable an instance of a class to free up any resources it has assigned
- reference counting allows more than one reference to a class instance

**Definition Syntax**

```
struct SomeStructure {
    // structure definition goes here
}
class SomeClass {
    // class definition goes here
}

struct Resolution {
    var width = 0
    var height = 0
}
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
```

**Structure and Class Instances**

The class and structure in the previous section only describe what those will look like, they don't describe a specific resolution or video mode. In order to do that you need an instance...

```
let someResolution = Resolution()
let someVideoMode = VideoMode()
```

**Accessing Properties**

Can access the properties of an instance using dot syntax...

```
print("The width of someResolution is \(someResolution.width)")
// Prints "The width of someResolution is 0"
```

You can go further down...

```
print("The width of someVideoMode is \(someVideoMode.resolution.width)")
// Prints "The width of someVideoMode is 0"
```

You can also use dot syntax to assign a new value to a variable property...

```
someVideoMode.resolution.width = 1280
print("The width of someVideoMode is now \(someVideoMode.resolution.width)")
// Prints "The width of someVideoMode is now 1280"
```

**Memberwise Initializers for Structure Types**

All structures have auto generated _memberwise initializer_, which can be used ot initialize member properties of new structure instances.

```
let vga = Resolution(width: 640, height: 480)
```

#####Structures and Enumerations are Value Types

A value type is a type whose value is copied when it's assigned to a variable or constant, or when it's passed to a function.

Below, a copy of hd(Resolution) is made, and is assigned to cinema...

```
let hd = Resolution(width: 1920, height: 1080)
var cinema = hd
```

If you change cinema width, hd width remains the same because of the copy...

```
cinema.width = 2048

print("cinema is now \(cinema.width) pixels wide")
// Prints "cinema is now 2048 pixels wide"

print("hd is still \(hd.width) pixels wide")
// Prints "hd is still 1920 pixels wide"
```

The same behavior applies to enumerations...

```
enum CompassPoint {
    case north, south, east, west
    mutating func turnNorth() {
        self = .north
    }
}
var currentDirection = CompassPoint.west
let rememberedDirection = currentDirection
currentDirection.turnNorth()

print("The current direction is \(currentDirection)")
print("The remembered direction is \(rememberedDirection)")
// Prints "The current direction is north"
// Prints "The remembered direction is west"
```

#####Classes Are Reference Types

Unlike value types, reference types are not copied when they are assigned to a variable or constant or when they are passed to a function...

```
let tenEighty = VideoMode()
tenEighty.resolution = hd
tenEighty.interlaced = true
tenEighty.name = "1080i"
tenEighty.frameRate = 25.0

let alsoTenEighty = tenEighty
alsoTenEighty.frameRate = 30.0

print("The frameRate property of tenEighty is now \(tenEighty.frameRate)")
// Prints "The frameRate property of tenEighty is now 30.0"
```

**Identity Operators**

```
if tenEighty === alsoTenEighty {
    print("tenEighty and alsoTenEighty refer to the same VideoMode instance.")
}
// Prints "tenEighty and alsoTenEighty refer to the same VideoMode instance."
```

####Properties

Properties associate values with a particular class, structure, or enumeration.

#####Stored Properties

A stored property is a constant or variable that is stored as part of an instance of a particular class or structure.

- Can be stored via variable or constant

```
struct FixedLengthRange {
    var firstValue: Int
    let length: Int
}
var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)
// the range represents integer values 0, 1, and 2
rangeOfThreeItems.firstValue = 6
// the range now represents integer values 6, 7, and 8
```

**Stored Properties of Constant Structure Instances**

If you create an instance of a struct and assign that instance to a constant, you cannot modify the instance's properties - even if declared as variables

```
let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
// this range represents integer values 0, 1, 2, and 3
rangeOfFourItems.firstValue = 6
// this will report an error, even though firstValue is a variable property
```

The same is not true for classes because they are reference types.

**Lazy Stored Properties**

- A property whose initial value is not calculated until the first time it is used
- useful when initial value for a property is dependent on outside factors whose values are not known until after an instance initialization is complete
- useful when initali value for a prop requires complex or computationally expensive setup that should not be performed unless or until needed

```
class DataImporter {
    /*
    DataImporter is a class to import data from an external file.
    The class is assumed to take a nontrivial amount of time to initialize.
    */
    var filename = "data.txt"
    // the DataImporter class would provide data importing functionality here
}

class DataManager {
    lazy var importer = DataImporter()
    var data = [String]()
    // the DataManager class would provide data management functionality here
}

let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")
// the DataImporter instance for the importer property has not yet been created
```

to retrieve data you must call importer from example above...

```
print(manager.importer.filename)
// the DataImporter instance for the importer property has now been created
// Prints "data.txt"
```

**Stored Properties and Instance Variables**

All infomration about the property - including name, type, and memory management characteristics - is definied in a single location as part of the type's definition.

#####Computed Properties

#####Property Observers

- observe and respond to changes in a porperty's value
- called every time a prop value is set, even if the new value is the same
- can add to anny stored properties except lazy properties
- `willSet` is called just before the value is stored
- `didSet` is called immediately after the new value is stored

```
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue  {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// About to set totalSteps to 200
// Added 200 steps
stepCounter.totalSteps = 360
// About to set totalSteps to 360
// Added 160 steps
stepCounter.totalSteps = 896
// About to set totalSteps to 896
// Added 536 steps
```

#####Global and Local Variables

- Global variables are defined outside of any function, method, closure, or type context
- Local variables are defined within a function, method, or closure context

#####Type Properties

- instance properties belong to an instance of a particular type, every time you create a new instance of that type, it has its own set of property values, separate form any other instance
- can also define properties that belong to the type itself and not to any one instance of that type, these are called type properties
  - useful for defining values universal to all instances of a particular type
  - can be variables or constants
  - computed properties are declared as variable properties

**Type Property Syntax**

- type properties are written as part of the type's definition, within the outer curly braces
- each type property is scoped to the type it supports
- definied with the `static` keyword
  - can use the `class` keyword instead to allow subclasses to override the superclass's implementation

```
struct SomeStructure {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 1
    }
}
enum SomeEnumeration {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 6
    }
}
class SomeClass {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 27
    }
    class var overrideableComputedTypeProperty: Int {
        return 107
    }
}
```

**Querying and Setting Type Properties**

- queried and set with dot syntax on the _type_, not the _instance_ of the type

```
print(SomeStructure.storedTypeProperty)
// Prints "Some value."
SomeStructure.storedTypeProperty = "Another value."
print(SomeStructure.storedTypeProperty)
// Prints "Another value."
print(SomeEnumeration.computedTypeProperty)
// Prints "6"
print(SomeClass.computedTypeProperty)
// Prints "27"
```

More indepth example with observers for an audio left and right channel level...

```
struct AudioChannel {
    static let thresholdLevel = 10
    static var maxInputLevelForAllChannels = 0
    var currentLevel: Int = 0 {
        didSet {
            if currentLevel > AudioChannel.thresholdLevel {
                // cap the new audio level to the threshold level
                currentLevel = AudioChannel.thresholdLevel
            }
            if currentLevel > AudioChannel.maxInputLevelForAllChannels {
                // store this as the new overall maximum input level
                AudioChannel.maxInputLevelForAllChannels = currentLevel
            }
        }
    }

// making a left and right channel
var leftChannel = AudioChannel()
var rightChannel = AudioChannel()

leftChannel.currentLevel = 7
print(leftChannel.currentLevel)
// Prints "7"
print(AudioChannel.maxInputLevelForAllChannels)
// Prints "7"

rightChannel.currentLevel = 11
print(rightChannel.currentLevel)
// Prints "10"
print(AudioChannel.maxInputLevelForAllChannels)
// Prints "10"
```

####Methods

#####Instance Methods

- support functionality of instances by providing ways to access and modify or provide functionality

```
class Counter {
    var count = 0
    func increment() {
        count += 1
    }
    func increment(by amount: Int) {
        count += amount
    }
    func reset() {
        count = 0
    }
}

//increment() increments the counter by 1.
//increment(by: Int) increments the counter by a specified integer amount.
//reset() resets the counter to zero.
```

Call instance methods with dot syntax

```
let counter = Counter()
// the initial counter value is 0
counter.increment()
// the counter's value is now 1
counter.increment(by: 5)
// the counter's value is now 6
counter.reset()
// the counter's value is now 0
```

**The Self Property**

- every instance of a type has an implicit property called self which is equal to the instance itself
- use self property to refer to current instance within own instance methods

Could rewrite above increment method as...

```
func increment() {
    self.count += 1
}
```

If you don't explicitl write self, Swift assumes it unless a parameter name is the same as a property of that instance...

```
struct Point {
    var x = 0.0, y = 0.0
    func isToTheRightOf(x: Double) -> Bool {
        return self.x > x
    }
}
let somePoint = Point(x: 4.0, y: 5.0)
if somePoint.isToTheRightOf(x: 1.0) {
    print("This point is to the right of the line where x == 1.0")
}
// Prints "This point is to the right of the line where x == 1.0"
```

**Modifying Value Types from Within Instance Methods**

- structures and enumerations are value types
- by default, properties of a value type can't be modified from its instance methods

Can mutate behavior, and any changes are written back to the original structure when method ends.

```
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveBy(x: 2.0, y: 3.0)
print("The point is now at (\(somePoint.x), \(somePoint.y))")
// Prints "The point is now at (3.0, 4.0)"
```

Calling it on a constant will report an error

```
let fixedPoint = Point(x: 3.0, y: 3.0)
fixedPoint.moveBy(x: 2.0, y: 3.0)
// this will report an error
```

**Assigning to self Within a Mutating Method**

#####Type Methods

- A method called on the type itself, indicated by `static` keyword before the method's `func` keyword
- called with dot syntax on the type, not the isntance of the type

```
class SomeClass {
    class func someTypeMethod() {
        // type method implementation goes here
    }
}
SomeClass.someTypeMethod()
```

Example

```
struct LevelTracker {
    static var highestUnlockedLevel = 1
    var currentLevel = 1

    static func unlock(_ level: Int) {
        if level > highestUnlockedLevel { highestUnlockedLevel = level }
    }

    static func isUnlocked(_ level: Int) -> Bool {
        return level <= highestUnlockedLevel
    }

    @discardableResult
    mutating func advance(to level: Int) -> Bool {
        if LevelTracker.isUnlocked(level) {
            currentLevel = level
            return true
        } else {
            return false
        }
    }
}

class Player {
    var tracker = LevelTracker()
    let playerName: String
    func complete(level: Int) {
        LevelTracker.unlock(level + 1)
        tracker.advance(to: level + 1)
    }
    init(name: String) {
        playerName = name
    }
}

var player = Player(name: "Argyrios")
player.complete(level: 1)
print("highest unlocked level is now \(LevelTracker.highestUnlockedLevel)")
// Prints "highest unlocked level is now 2"

player = Player(name: "Beto")
if player.tracker.advance(to: 6) {
    print("player is now on level 6")
} else {
    print("level 6 has not yet been unlocked")
}
// Prints "level 6 has not yet been unlocked"
```

####Subscripts

####Inheritance

A class can inherit methods, properties, and other characteristics from another class
- class that inherits is subclass, subclass inherits from superclass
- classes can call methods, properties, and subscripts from their superclass and can provide overriding versions of them
- classes can add property observers to inherited properties to be notified when the value of a property changes

#####Defining a Base Class

```
class Vehicle {
    var currentSpeed = 0.0
    var description: String {
        return "traveling at \(currentSpeed) miles per hour"
    }
    func makeNoise() {
        // do nothing - an arbitrary vehicle doesn't necessarily make a noise
    }
}

// create new instance with initializer syntax
let someVehicle = Vehicle()

//can access description property
print("Vehicle: \(someVehicle.description)")
// Vehicle: traveling at 0.0 miles per hour
```

#####Subclassing

To indicate that a subclass has superclass, write subclass name before superclass name separated by colon

```
class SomeSubclass: SomeSuperclass {
    // subclass definition goes here
}

// Example
class Bicycle: Vehicle {
    var hasBasket = false
}

let bicycle = Bicycle()
bicycle.currentSpeed = 15.0
print("Bicycle: \(bicycle.description)")
// Bicycle: traveling at 15.0 miles per hour
```

#####Overriding

A subclass can provide its own implementation of an instance/type method, instance/type property, or subscript it would otherwise inherit from superclass

- to override a characteristic, you prefix your overriding definition with the `override` keyword

**Accessing Superclass Methods, Properties, and Subscripts**

Access the superclass version of a method, property, or subscript by using the super prefix

  - An overridden method named someMethod() can call the superclass version of someMethod() by calling super.someMethod() within the overriding method implementation
  - An overridden property called someProperty can access the superclass version of someProperty as super.someProperty within the overriding getter or setter implementation
  - An overridden subscript for someIndex can access the superclass version of the same subscript as super[someIndex] from within the overriding subscript implementation

**Overriding Methods**

You can override an inherited instance or type method to provide a tailored or alternative implementation of the method within your subclass

```
// define new subclass of Vehicle called Train, which overrides the makeNoise() method that train inherits from Vehicle

class Train: Vehicle {
    override func makeNoise() {
        print("Choo Choo")
    }
}

let train = Train()
train.makeNoise()
// Prints "Choo Choo"
```

**Overriding Properties**

Can override instance/type property to provide your own custom getter and setter for that property, or to add property observers to enable overriding property to observe when the underlying property value changes

- must always state the name AND the type of the property you're overriding, to enable the compiler to check that your override matches a superclass property with the same name and type

```
class Car: Vehicle {
    var gear = 1
    override var description: String {
        return super.description + " in gear \(gear)"
    }
}

let car = Car()
car.currentSpeed = 25.0
car.gear = 3
print("Car: \(car.description)")
// Car: traveling at 25.0 miles per hour in gear 3
```

**Overriding Property Observers**

Can use property overriding to add property observers to an inherited property - to know when value of inherited property changes

```
class AutomaticCar: Car {
    override var currentSpeed: Double {
        didSet {
            gear = Int(currentSpeed / 10.0) + 1
        }
    }
}

let automatic = AutomaticCar()
automatic.currentSpeed = 35.0
print("AutomaticCar: \(automatic.description)")
// AutomaticCar: traveling at 35.0 miles per hour in gear 4
```

**Preventing Overrides**

Can prevent a method, property, or subscript being overriden by marking it as final, achieved by writing `final` modifier before the method/prop/subscript's introducer keyword
  - can also mark an entire class as final by writing the `final` modifier before the `class` keyword in the class definition ex. `final class Vehicle`

####Initialization

Process of preparing instance of a class, structure or enumeration for use
  - Swift initializers don't return a value

#####Setting Initial Values for Stored Properties

Classes and structures must set all stored properties to an appropriate value by the time an instance of that class or structure is created

**Initializers**

Called to create a new instance of a particular type...

```
init() {
    // perform some initialization here
}

// example

struct Fahrenheit {
    var temperature: Double
    init() {
        temperature = 32.0
    }
}
var f = Fahrenheit()
print("The default temperature is \(f.temperature)° Fahrenheit")
// Prints "The default temperature is 32.0° Fahrenheit"
```

**Default Property Values**

Alternatively, you can specify a default property value as part of the property's declaration...

```
struct Fahrenheit {
    var temperature = 32.0
}
```

#####Customizing Initialization

Can customize initialization process with input parameters and optional property types, or by assigning constant properties during initialization...

**Initialization Parameters**

```
// two custom initializers fromFahrenheit/fromKelvin

struct Celsius {
    var temperatureInCelsius: Double
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
}

let boilingPointOfWater = Celsius(fromFahrenheit: 212.0)
// boilingPointOfWater.temperatureInCelsius is 100.0
let freezingPointOfWater = Celsius(fromKelvin: 273.15)
// freezingPointOfWater.temperatureInCelsius is 0.0
```

**Parameter Names and Argument Labels**

Parameters can have a name for use within the initializer's body and an argument label for use when calling the initializer

Swift provides an automatic label for every parameter in an initializer if you don't provide one

```
struct Color {
    let red, green, blue: Double
    init(red: Double, green: Double, blue: Double) {
        self.red   = red
        self.green = green
        self.blue  = blue
    }
    init(white: Double) {
        red   = white
        green = white
        blue  = white
    }
}

// can use both initializers to create a new color instance...

let magenta = Color(red: 1.0, green: 0.0, blue: 1.0)
let halfGray = Color(white: 0.5)

// not possible to call them without the argument labels...

let veryGreen = Color(0.0, 1.0, 0.0)
// this reports a compile-time error - argument labels are required
```

**Initializer Parameters Without Argument Labels**

If you don't want to use an arg label for an initializer parameters, write an underscore `_` instead of an explicit argument label for that parameter to override default behavior

```
struct Celsius {
    var temperatureInCelsius: Double
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
    init(_ celsius: Double) {
        temperatureInCelsius = celsius
    }
}
let bodyTemperature = Celsius(37.0)
// bodyTemperature.temperatureInCelsius is 37.0
```

**Optional Property Types**

If custom type is allowed to/has 'no value' - declare the property with an optional type, which is automatically initialized with a value of nil indicating the property is intended to not have a value yet

```
class SurveyQuestion {
    var text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        print(text)
    }
}
let cheeseQuestion = SurveyQuestion(text: "Do you like cheese?")
cheeseQuestion.ask()
// Prints "Do you like cheese?"
cheeseQuestion.response = "Yes, I do like cheese."
```

**Assigning Constant Properties During Initialization**

Can assign a value to a constant property at any point during initialization, as long as it is set to a definite value by time initialization finishes
  - once a constant property is assigned a value, it can't be further modified

```
class SurveyQuestion {
    let text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        print(text)
    }
}
let beetsQuestion = SurveyQuestion(text: "How about beets?")
beetsQuestion.ask()
// Prints "How about beets?"
beetsQuestion.response = "I also like beets. (But not with cheese.)"
```

#####Default Initializers

Swift provides a default initializer for any structure or class that provides default values for all of its properties and does not provide at least one initializer itself
  - it simply creates a new instance with all properties set to default values

  ```
  class ShoppingListItem {
    var name: String?
    var quantity = 1
    var purchased = false
}
var item = ShoppingListItem()
```

**Memberwise Initializers for Structure Types**

Structure types automatically receive a memberwise initializer if they don't define any of their own custom initializers
  - unlike default initializers, the structure receives memberwise initializer even if it has stored properties that do not have default values

```
struct Size {
    var width = 0.0, height = 0.0
}
let twoByTwo = Size(width: 2.0, height: 2.0)

// automatically receives init(width:height:) memberwise initializer, which you can use to initialize a new Size instance
```

#####Initializer Delegation for Value Types

#####Class Inheritance and Initialization

#####Failable Initializers

#####Required Initializers

#####Setting a Default Property Value with a Closure or Function
