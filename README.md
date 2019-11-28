
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
