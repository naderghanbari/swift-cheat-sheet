
# Swift Language Guide Cheat Sheet

<details>
<summary>Constants and Variables</summary>

```swift
let aspectRatio = 1.6                     // Constant, Inferred Type

var remainingTime = 60                    // Variable, Inferred Type

var userName: String = "john@doe.com"     // Variable, Annotated Type

let age = 10, name = "John"               // Multiple Constants, Inferred Type

var x, y, z: Double                       // Multiple Variable Declarations, The same Annotated Type

var x = 0, y = 0, z = 0                   // Multiple Variable Initializations, Inferred Type

typealias Distance = Int64                // Type Alias
```
</details>

<details>
<summary>Relations and Logical Operations</summary>

```swift

obj1 == obj2                              // Equality check

obj1 != obj2                              // Not-Equals check

if 2 < 3, i <= 5, i > 7, i >= 8           // Usual order relations
```
</details>

<details>
<summary>String</summary>

```swift
print(welcomeMessage)                     // Print, Acts like println by default

print("My name is \(userName)")           // String Interploation, Basic 

let longString = """                      // Multi-line Strings
  Long multiline 
  string.
  """                                     // Closing quote determines the alignment (no need for strip)

let immutableString = "no can change"     // Constant strings are immutable

var changeMeLater = "Yes, "               // Variable strings are mutable
chaneMeLater += "We Can!"

let exclamationMark: Character = "!"      // Character type, Chracter String literal (no single quotes)

let unicode = "Penguin 🐧"                // Unicode

let s = "Guten Tag!"                      // Indexing
s[s.startIndex]                           // G
s[s.index(before: s.endIndex)]            // !
s[s.index(after: s.startIndex)]           // u

for character in "Dog!🐶" {               // Iterate over characters 
  print(character)
}

let threeMoreDoubleQuotationMarks = #"""  // Escape from escaping!
Here are three more double quotes: """
"""#
```

</details>

<details>
<summary>Numeric Types</summary>

```swift
let minValue: UInt8 = UInt8.min           // Unsigned Integer, a la C types

let largeNumber: Int = 102334             // Platform-specific, Either Int32 or Int64

let highPrecision: Double = 2.718182198   // 64-bit floating point number 

let ascpetRatio: Float = 1.333333         // 32-bit floating point number 
```

</details>

<details>
<summary>Booleans</summary>

```swift
let thisIsATautology: Bool = true         // Bool type for booleans, true litreal

let examFailed = false                    // `false` literal 

let isSafe = zombiesCount == 0            // Equality comparison operator ==

if isSafe { print("No worries") }         // Conditional 
else { print("Run!") }
```

</details>

<details>
<summary>Tuples</summary>

```swift
let binding = ("localhost", 8080)         // 2-Tuple Construction, Inferred Type (String, Int)

let p: (Int, Int, Int) = (1, 3, 5)        // 3-Tuple Construction, Annotated Type

let (x, y, z) = coordinates               // Deconstruction

let (host, _) = binding                   // Discarding extra information with _

print("Host: \(binding.0)")               // Accessing the First component (0-based index)
print("Port: \(binding.1)")               // Accessing the Second component

let user = (name: "John", age: 10)        // Named tuples

print("User name: \(user.name)")          // Accessing named component

(b, a) = (a, b)                           // Trick to swap two variables!

(10, "Zebra") < (10, "Apple")             // Component-wise left-to-right comparison
```

</details>

<details>
<summary>Optionals</summary>

```swift
var maybeNumber: Int?                     // A type qualified with a `?` means optional

maybeNumber = nil                         // `nil` indicates absence of a value

var policyNoOpt: String?                  // Initial value is `nil` for uninitialized variables

policyNoOpt = "#FF2345"                   // Assign an actual value, indicates presense of a value

if (maybeNumber != nil) {                 // Presence of value Check
  let num = maybeNumber!                  // Access value by forcing matters using !
  print("Lucky number is: \(num)")        // Forcing throws runtime error if value is nil
}

if let policyNo = policyNoOpt {           // Optional Binding, checks presence and binds
  print("Policy No: \(policyNo)")         // the actual value, if any, 
}                                         // at the same time (a la monadic map)

if var name = nameOpt,                    // Multiple Optional Bindings
   let age = ageOpt,                      // Unpacking to a variable or constant is allowed
   age > 2 {                              // Using unpacked value in more conditionals is allowed
     name = "Passenger \(name)"           // Condition fails if any of optionals are nil or
     print("\(name): \(age)")             // if subsequent constraints don't hold
}

var email: String!                        // Implicitly Unwrapped Optional, Type qualified by !
email = "john@doe.com"                    // Initialization, Most probably in a class constructor
print(email)                              // Auto-unwrapped, email acts as email! everyhwere

maybeNumber ?? 0                          // Nil Coalesce, Like maybeNumber.getOrElse(0) in Scala
```

</details>

<details>
<summary>Error Handling</summary>

```swift

func getPermission() throws  {            // Indicates a possibility of throwing errors
  throw Permissions.deniedByUser          // Throws an error
}

do {                                      // Error handling
  try getUserPermission()
} catch Permissions.deniedByUser {
  // handle error
} catch Permissions.deniedByAdmin(let name) where name == "CEO" {
  println("Ohhhkay")
} catch catch Permissions.deniedByAdmin(let name) {
  println("Gotcha \(name)! ")
}

let x = try? someThrowingFunction()      // Convert Errors to Optionals

let photo = try! someThrowingButSound()  // Disables error propagation, aka "I'm sure it never fails" 

assert(age >= 0, "Unexpected!")          // Assertions
precondition(index > 0, "Must be true")  // Preconditions, compiler flag dependent
```

</details>

<details>
<summary>Ranges</summary>

```swift

for index in 1...5 {                     // a..b is the inclusive range [a, b]
    print("\(index)")                    // 1, 2, 3, 4, 5
}

a..<b                                    // [a, b) half-open range, includes a, excludes b

myArray[2...]                            // One-Sided range, Array Slicing a la Python's myArray[2:]
myArray[...2]                            // One-Sided inclusive range, myArray[:3] in Python
myArray[..<2]                            // One-Sided exclusive range, myArray[:2] in Python
```

</details>

<details>
<summary>Collections: Arrays</summary>

```swift
var arr: Array<Int>                      // Mutable array of integers, var signals mutability

var arr: [Int] = []                      // Shorthand and preferred notation for array types

["a", "b", "c"]                          // Array Literal

arr.append(1)                            // Append an element
arr += [1, 2]                            // Append an array to the end of this array

arr1 + arr2                              // Concatenate two arrays

arr.count                                // Size of the array
arr.isEmpty                              // Emptiness check

arr[0]                                   // Access elements, Subscript syntax

arr[0] = "NewValue"                      // Update element at a specific index

const justRemoved = arr.remove(at: 2)    // Remove the item at index 2 and return it
const wasLast = arr.removeLast()         // Remove last element from array

for item in shoppingList {               // Iterate over an array
  print(item)
}

for (idx, elem) in arr.enumerated() {   // Iterate with index
    print("Item \(idx + 1): \(elem)")
}

myArray[2...]                            // One-Sided range, Array Slicing a la Python's myArray[2:]
myArray[...2]                            // One-Sided inclusive range, myArray[:3] in Python
myArray[..<2]                            // One-Sided exclusive range, myArray[:2] in Python
```

</details>

<details>
<summary>Collections: Sets</summary>

```swift
var mySet: Set<SomeType>                // Set type, SomeType must be Hashable

var letters = Set<Character>()          // Empty set

const genres: Set = ["Rock", "Jazz"]    // Array litreal can be used for sets

letters.insert("b")                     // Add a new member

letters.count                           // Size of the set

letters.contains("c")                   // Membership, indicator function of the set

setA.intersection(setB)                 // Set-theoric functions
setA.symmetricDifference(setB)
setA.union(setB)
setA.subtracting(setB)
setA.isSubset(of: setB) 
setA.isSuperset(of: setB) 
setA.isStrictSubset(of: setB) 
setA.isStrictSuperset(of: setB) 
setA.isDisjoint(with: setB) 
```

</details>

<details>
<summary>Collections: Dictionaries</summary>

```swift
var dict: Dictionary<String, String>    // Dictionary<Key, Value>

var population: [String: Int]           // Shorthand and preferred type notation

var population = [String: Int]()        // Empty dictionary with explicit types

population = [:]                        // Empty set litreal for an already proven type

["Earth": 42, "Mars": 1, "Moon": -14]   // Dictionary literal   

population["Earth"] = 42                // Assign value to key

                                        // Alternative syntax for updating
const oldVal: Int? = population.updateValue(43, forKey: "Earth")

if let old = population.updateValue(43, forKey: "Earth") {
  print("The old value for Earth was \(old).")
}

population.removeValue(forKey: "Earth") // Remove a key

population["Earth"] = nil               // Syntactic sugar for removing a key

const p: Int? = population["Moon"]      // Access values for a key, if any

for (where, howMany) in population {    // Iterate over <K,V> pairs
  print("\(where): \(howMany)")
}

population.keys                         // Keys set
population.values                       // Values set

[String](population.keys.sorted())      // Convert the key set to a sorted array
```

</details>

<details>
<summary>Switch</summary>

```swift
switch someCharacter {                  
  case "a": print("The first letter of the alphabet")
  case "z": print("The last letter of the alphabet")
  default : print("Some other character")
}

// No fall through
// First match wins
// Must be exhaustive, that is should always match any value of the target type
// Compile error if switch is not exhaustive, very helpful

swith someCharacter {
  case "a", "A": print("A or a")       // Either "a" or "A"  
}

switch approximateCount {
  case 0     : naturalCount = "no"
  case 1..<5 : naturalCount = "a few"  // Range matching
} 

let anotherPoint = (2, 0)             
switch anotherPoint {       
  case (let x, 0):                     // Binding and partial matcing
    print("on x-axis \(x)")
  case (0, let y):
    print("on y-axis (y)")
  case let (x, y) where x == y:        // Where clause for bound variables
    print("on the diagnoal")
  case let (x, y):
    print("any other case") 
} 

ler origin = (0, 0)
let myPoint = (9, 0)
switch myPoint {
  case origin:                         // Value match: checks equality
    print("Is Origin")
  case (let dist, 0), (0, let dist):   // Compound case with binding: all of the same type
    print("On an axis, \(dist) ")      // If it doesn't make sense at first sight, play with it 
  default:
    print("Not on an axis")
} 
```

</details>

<details>
<summary>Control Flow</summary>
    
```swift
for char in input {
  if char == "a" {
    continue                            // Skip the rest of current and go to next iteration
  }
  process(char)
}


for char in input {
  if char == "E" {
    break                               // Break out of the whole loop
  }
  process(char)
}
print("E pressed, game over!")

let myInt = 5
var description = "\(myInt) is"
switch myInt {
  case 1:
   break                                // Match and ignore case using break
  case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " is prime, and also"
    fallthrough                         // Falls through to next case, like C
  default:
    description += " an integer."
}
// prints "5 is prime and also an integer"


func greet(user: [String: String]) {
  guard let name = user["name"] else {  // Guard statement 
    return                              // Early exit pattern
  }

  print("Hello \(name)!")

  guard let loc = user["loc"] else {    // Watch out, another guard!
    print("Where are you?")             // Another not so early exist
    return
  }

  print("Weather is nice in \(loc).")
}
```

</details>

<details>

<summary>Functions</summary>

```swift
func abs(x: Int) -> Int {               // Defining a function of type Int -> Int
  return x < 0 ? -x : x 
}

abs(x: -3)                              // Calling the function, naming the param is required

                                        // A function that returns an optional tuple
func minMax(array: [Int]) -> (min: Int, max: Int)? {
  if array.isEmpty {
    return nil
  }
  // Find min and max is array is not empty
  return (min, max)
}

                                        // Calling the function
if let bounds = minMax(array: [8, -6, 2, 109, 3, 71]) {
  print("min is \(bounds.min) and max is \(bounds.max)")
}

func sgn(x: Int) -> Int {               // Implicit Return
  x < 0 ? -1 : x > 0 ? 1 : 0            // If the entire body is a single expression, there
}                                       // is no need for the "return" keywrod

                                        // Argument label "from"
                                        // Parameter name "hometown"
func greet(person: String, from hometown: String) -> String {
  "You're from \(hometown)."            // Parameter name is used in the body
}

greet(person: "Joe", from: "Montreal")  // Argument label is used at call site
                                        // By default param name is used as the arg label
                                        // Like "person" param in this function

func abs(_ x: Int) -> Int {             // Omitting the arg label
  x < 0 ? -x : x 
}

abs(4)                                  // Now "abs" can be called wihtout any label

                                        // Default values for parameters
func dockerPort(host: String = "localhost", port: Int = 80) -> Int {
  // function body
}

func mean(_ arr: Double...) -> Double { // Variadic params, like Varargs in Java 
  var total: Double = 0                 // At mpst one varaidic arg is allowed per function
  for number in numbers {               // Type of variadic arg "arr" is [Double]
    total += number
  }
  return total / Double(numbers.count)
}

mean(1, 2, 3, 4)

                                        // inout params, annotated by putting the 
                                        // "inout" keyword before the type
                                        // Indicates that the param is passed as a mutable reference.
                                        // Please avoid this at all costs!  
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
  let temporaryA = a
  a = b
  b = temporaryA
}

var someInt = 3
var anotherInt = 107                    // Only mutable vars are allowed as inout params
swapTwoInts(&someInt, &anotherInt)      // Prefixing with & is required for inout vars

func add(_ a: Int, _ b: Int) -> Int {   // Type of this function is (Int, Int) -> Int
  return a + b
}

var myFunc: (Int, Int) -> Int = add     // Function variable, 
                                        // For λ calculus geeks: Eta conversion 

                                        // Higher order function
func hof(_ adder: (Int, Int) -> Int, _ a: Int, _ b: Int) -> Int {
  adder(a, b)    
}
                                        // Nested functions, and returning functions
func choose(dir: Bool) -> (Int) -> Int {
  func forward(_ x: Int) -> Int { x + 1 }
  func backward(_ x: Int) -> Int {x - 1 }
  return dir ? forward : backward
}

func sideEffect() {                     // Type of this function is () -> Void or () -> ()
  print("Hello")                        // () indicates no input params and also is an alias for Void 
}                                       // Void is the same as Unit in Haskell and Scala
                                        // If you find it confusing that Unit in Haskell is Void in 
                                        // Swift and the Void type in Haskell is 
                                        // a totally different thing, then congrats, you are a 
                                        // normal person. 
                                        // Keywords for search: "Initial and Terminal objects"  
                                        
```

</details>

<details>
<summary>Closures, aka Lambdas</summary>

```swift
let nums = [1, 5, 3, 4]

                                        // "by" is a lambda passed to the sorted function
                                        // syntax : { (Params) -> ReturnType in expr } 
nums.sorted(by: { (x: Int, y: Int) -> Bool in x < y })

nums.sorted(by: { x, y in x < y })      // Inferred types and implicit return, short and nice!

                                        // Bash and Perl fans, brace for impact
names.sorted(by: { $0 > $1 } )          // Shorthand notation, $0 for 1st arg, $1 the 2nd and so on  

names.sorted(by: >)                     // Operator methods, String::< in this case   
names.sorted(by: <)                     // Beautiful and simple and type-safe at the same time
                                        // Not as powerful as type-classes in Haskell or Scala, but it'll do

names.sorted { $0 > $1 }                // Trailing closure syntax
                                        // At call site if the last arg of a function call is
                                        // a closure, it can be passed in after the parens or 
                                        // after the function name if there's no parens

nums.map { x in x * 2 }                 // Another example with the map method of arrays


var globalHandlers: [() -> ()]
                                        // @escaping is needed if the closure escapes 
                                        // Compiler is rightfully very strict, no surprises like youKnowWho.js
func register(handler: @escaping () -> ()) {
  globalHandlers.append(handler)
}

                                        // AutoClosures, aka Call-by-Name
                                        // Passed param won't be evaluated until and if used
                                        // in the body at runtime
func serve(customer customerProvider: @autoclosure () -> String) {
  print("Now serving \(customerProvider())!")
}
                                        // Because customer is an autoclosure we can pass it
                                        // like a regular param without parens
serve(customer: customersInLine.remove(at: 0))
```

</details>

<details>
<summary>Enums</summary>

```swift
enum CompassPoint {                     // Enum type
  case north                            // Enum case            
  case south                            // Unlike C, there's no integer value by default
  case east
  case west
}

enum Direction {
  case up, left, down, right            // Multiple comma-separated cases    
}

let nextMove = Direction.up             // Using it with a fully qualified name

var dir: CompassPoint                   
dir = .north                            // Shorthand, works only if the type is known

switch dir {                            // Pattern matching on enums
  case .north: print("Us")              // Must be exhaustive as usual
  case .south: print("Them")
  case .east:  print("Far")
  case .west:  print("Also us")
}  

enum Drink: CaseIterable {              // Makes it iterable
  case coffee, tea, juice
}
let all: [Drink] = Drink.allCases       // allCases return the array of all cases


enum TwoFactorAuthMethod {              // Enums cas be used for ADTs
  case disabled
  case phone(String)                    // Associated values, works like tuples, can be named
  case textMessage(String)      
  case google(token: String, time: Int)
  case accessCodes(codes: [String])     
  case email(String, secondary: String)
}

var method: TwoFactorAuthMethod
method = .phone("+1-111-111111")        // Passing associated values, just like tuples
method = .accessCodes(codes: ["1", "2"])
method = .disabled

switch method {                         // Pattern matching on ADTs                
  case .disabled:                    
    print("No way!")
  case .phone(let number):              // Binding the associated value, think tuples
    print(number)
  case let .accessCodes(codes):         // Let or var can be placed before case name 
    print(codes.count)
  case .email:                          // Associated values can be ignored    
    print("Temporarily unsupported")
  default:
    print("Other methods are not supported yet!") 
}

enum ASCII: Character {                 // Raw values, lifting value types to enums
  case tab = "\t"                       // Each raw value must be unique
  case lf = "\n"                        // Compiler asserts this because it's smart and it
  case cr = "\r"                        // knows how to distinguish different literals!
}

                                        // Implicit raw values
                                        // Each case's raw value is the previous' + 1
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}
extension Planet: CaseIterable {}       // Making it iterable using extensions 

Planet.earth.rawValue                   // Accessing raw values

enum CompassPoint: String {             // For String raw values, the name of each
    case north, south, east, west       // case is implicitly assigned as the raw value
}

CompassPoint.north.rawValue             // "north"

                                        // Initializing from a raw value
                                        // Returns an optional, reasonably, because not 
                                        // all raw values necessarily correspond to an actual case
let maybe: Planet? = Planet(rawValue: 7)


                                        // And now, the super power of enums in Swift!
                                        // Recursive enumerations
enum Expr {
  case number(Int)
  indirect case add(Expr, Expr)         // indirect keyword is needed for recursive branches
  indirect case mul(Expr, Expr)
}

indirect enum Expr {                    // indirect keyword can be put before the enum
  case number(Int)                      // keyword which then applies to all cases with    
  case add(Expr, Expr)                  // associated values  
  case mul(Expr, Expr)
}

func eval(_ expr: Expr) -> Int {        // A recursive function
  switch expr {                         // Pattern matching recursive enums
    case let .number(value): return value
    case let .add(l, r): return eval(l) + eval(r)
    case let .mul(l, r): return eval(l) * eval(r)
  }
}
```

</details>

<details>
<summary>Structures, Value Types</summary>

```swift
struct Resolution {                     // Structs, similar to case classes in Scala
  var width = 0                         // A stored property with a default property value      
  var height = 0
}
                                        // Member-wise initializer
                                        // Compiler automatically generates it for structs
let vga = Resolution(width: 640, height: 480)

vga.width                               // Accessing properties of a struct

                                    
// Structs, enums, strings, inetegres, floats, and booleans are all value types
// When assigned to a variable or constant, they get copied

var currentResoltion = vga              // Gets copied, because right hand side is a value type

currentResoltion.width = 320            // Only the new copy is mutated 
vga.width                               // still 640, original copy is intact


vga.width = 100                         // Impossible! Compile error! Kaboom!
                                        // If a value type is assigned to a constant, none of 
                                        // its properties can be mutated, even if they are defined
                                        // as vars. This behavior is different for reference types.
```

</details>

<details>
<summary>Classes, Reference Types</summary>

```swift
class VideoMode {                       // Class definition
  var resolution = Resolution()         // Stored property
  var interlaced = false
  var frameRate = 0.0
  var name: String?
}

// Classes are reference types
// They don't get copied when assigned, all references of a class 
// point to the same instance

let tenEighty = VideoMode()             // Initialization
tenEighty.resolution = hd               // Set property 
tenEighty.interlaced = true             // Because classes are reference types, we can
tenEighty.name = "1080i"                // mutate mutable properties of an instance, even if
tenEighty.frameRate = 25.0              // that instance is a constant like tenEighty here

let alsoTenEighty = tenEighty           // Assign the instance to a new reference

alsoTenEighty.frameRate = 30.0          // Mutate the property via the new reference

tenEighty.frameRate                     // Is now 30.0

                                        // Triple equal signs is the "identical to" operator
                                        // Returns true if both references refer to exactly the
                                        // same class instance
                                        // Similar to == in Java (reference equality)
tenEighty === alsoTenEighty             // True

someOther !==  tenEighty                // Not idential to, Similar to != in Java
```

</details>

<details>
<summary>Properties</summary>

```swift

struct FixedLengthRange {               // Stored properties    
  var firstValue: Int                   // Variable stored property, can be mutated if the struct 
                                        // instance is a variable
  let length: Int                       // Constant stored property, can't be mutated even if
                                        // the struct instance is a variable
}

class DataManager {
  lazy var importer = DataImporter()    // Lazy stored properties, their initial value is 
  var data = [String]()                 // not calculated until the first time it is used
                                        // Opposite to Scala, in Swift only a var can be lazy
  func manage() {
    // use importer here
  }
}

struct Rect {
  var origin = Point()
  var size = Size()
  var center: Point {                   // Computed property, no storage just getter and setter
    get {                               // Compute the value from other properties
      let x = origin.x + (size.width / 2)
      let y = origin.y + (size.height / 2)
      return Point(x: x, y: y)
    }
    set(newCenter) {                    // Setter: sets values to other properties
      origin.x = newCenter.x - (size.width / 2)
      origin.y = newCenter.y - (size.height / 2)
    }
  }
}

struct Rect {
  var origin = Point()
  var size = Size()
  var center: Point {                   // A computed property can't be a constant     
    get {                               // Shorthand getter, no return needed for a single expression                 
      Point(x: origin.x + (size.width / 2), y: origin.y + (size.height / 2))
    }
    set {                               // Shorthand for setter (no explicit name for the param)
      origin.x = newValue.x - (size.width / 2)      // newValue is the implicit name for the param
      origin.y = newValue.y - (size.height / 2)
    }
  }
}

var square = Rect(origin: Point(x: 0.0, y: 0.0),
                  size: Size(width: 10.0, height: 10.0))

square.center = Point(x: 15.0, y: 15.0) // Setting a computed property

struct Cuboid {
  var width = 0.0, 
  var height = 0.0
  var depth = 0.0
  var volume: Double {                  // Read only computed property
    width * height * depth              // No setter. Getter can be omitted like here
  }
}


class StepCounter {                     // Property observers, a door to reactive programming 
  var total: Int = 0 {                  // A normal stored property with observers
    willSet(newTotal) {                 // Called right before a new value is stored
      print("Will set to \(newTotal)")  // Like componentWillUpdate in old versions of React
    }
    didSet {                            // Called immediately after value is stored
      if total > oldValue  {            // oldValue is the default param name if no override is given
        print("Added \(total - oldValue) steps")
      }
    }                                   // Similar to componentDidUpdate in React
  }
}

// Wrapped properties are not covered here

// Global variables are those that are defined outside of any class, struct, or function  
// Global variables can also be computed or stored and can have observers
// Global variables are always lazy! Unlike properties, global constants can, and always are, lazy

let myGlobal = expensive()              // Global, automatically lazy
```

</details>

<details>
<summary>Property Wrappers</summary>

```swift

// Write code that manages how a property is set and re-use it for multiple properties
// Defined in a struct, enum or class


@propertyWrapper                        // Annotation indicating a property wrapper definition
struct TwelveOrLess {
  private var number = 0                // Internal state of the propety wrapper (arbitrary)
  var wrappedValue: Int {               // wrappedValue is a special name, by-convention like oldValue in didSet
    get { number }                      // Getter logic
    set { number = min(newValue, 12) }  // Setter logic
  }
}

@TwelveOrLess var height: Int           // Usage, annotation before property declaration
print(height)                           // 0 
height = 10                             
print(height)                           // 10
height = 24
print(height)                           // 12


@propertyWrapper                        // A property wrapper with initializers 
struct SmallNumber {
  private var maximum: Int
  private var number: Int

  var wrappedValue: Int {
    get { number }
    set { number = min(newValue, maximum) }
  }

  init() {                              // Called when used as below
    maximum = 12                        // @SmallNumber var height: Int
    number = 0
  }
  init(wrappedValue: Int) {             // Called when assigned a value when initialized as below
    maximum = 12                        // @SmallNumber var height: Int = 8
    number = min(wrappedValue, maximum)
  }
  init(wrappedValue: Int, max: Int) {   // Used when params are passed as below variants
    self.maximum = max                  // @SmallNumber(max: 44) var height: Int = 23
    number = min(wrappedValue, max)     // @SmallNumber(wrappedValue: 23, max: 44) var height: Int
  }
}


@propertyWrapper
struct SmallNumber {
  private var number = 0
  var projectedValue = false            // Another convention, projectedValue allows accessing an additional
  var wrappedValue: Int {               // value or type using the $ syntax
    get { number }
    set {
      if newValue > 12 {
        number = 12
        projectedValue = true
      } else {
        number = newValue
        projectedValue = false
      }
    }
  }
}

@SmallNumber var x: Int
x = 4                                   // setter
x                                       // get wrapped value 4
$x                                      // get projected value (true)

@DbObject user: User                    // Another example
user.name                               // Wrapped value
$user.flushConnection()                 // Projected value can expose a lower-level object
                                        // Don't do that in practice, instead use proper designs like domain-driven
                                        // design but keep in mind that projected value is there and can be used
                                        // if it does not vioalte your code of honour
```

</details>

<details>
<summary>Type Properties</summary>

```swift
struct User {                               // Type properties belong to the type (struct or class), not instances
  static const placeholder = "John Doe"     // Like static final in C, and Java
  static var minAge: Int {                  // static computed property
    18
  }
}

class SomeClass {                           // Overridable computed type property (JVM langs are crying now!) 
  class var computed: Int {                 // keyword class has the same meaning as
    107                                     // static but it allows sub-classes to override the
  }                                         // computed property
}

enum Rejection {
  static var message = "You got rejected"   // Enums can also have type properties
  case noToken, badToken, expiredToken       
}

User.placeholder                            // Query the stored type property
User.minaAge = 21                           // Set the stored type property
```

</details>

<details>
<summary>Methods</summary>

```swift
                                        // Classes, Structs, and Enums can have instance methods

class Counter {
  var count = 0
  func increment() {                    // An instance method, defined exactly like a function
    count += 1 
  }
  func increment(by amount: Int) {      // Another instance method with named params
    count += amount
  }
  func exceeds(count: Int) {            // Param name is the same as the instance property name, self is needed
    self.count > count                  // self, is the instance itself, always implicitly available 
  }                                     // like self in Python and this in Java
  func reset() {
    count = 0
  }
}


struct Point {                          // Mutating a value type from an instance method
  var x = 0.0, y = 0.0                  // Method has to be qualified with the mutating keyword
  mutating func moveBy(x deltaX: Double, y deltaY: Double) {
      x += deltaX
      y += deltaY
  }
}

var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveBy(x: 2.0, y: 3.0)        // A mutating method can be called only on variables
                                        // Calling them on a constant gives a compile error

struct Point {
  var x = 0.0, y = 0.0
  mutating func moveBy(x deltaX: Double, y deltaY: Double) {
      self = Point(x: x + deltaX, y: y + deltaY)    // Big bang! Assign a new value to self is possible
  }
}

enum TriStateSwitch {
  case off, low, high
  mutating func next() {
    switch self {
      case .off : self = .low           // Assigning self in an enum is also possible
      case .low : self = .high
      case .high: self = .off
    }
  }
}
```

</details>
