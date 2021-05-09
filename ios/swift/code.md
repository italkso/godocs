# Coding in Swift

### 1. Grammer

#### struct

```swift
struct StructName {
    
	// Instance or Type Property, Stored or Computed Property, Lazy Property
    var property: Int
    
    //	Default Initializer, Custome Initializer
    init(property: Int) {
        self.property = property
    }
    
    //	Instance or Type Method, Mutating Method
    func someMethod() {
    	//
    }
}
```

#### enum

```swift
enum Optional {
	case none,some
}

enum CompassPoint {
    case north, south, east, west
    mutating func turnNorth() {
        self = .north
    }
}
```

#### class

```swift
class SomeBaseClass {
    // Definition of base class 
}

class SomeSubclass: SomeSuperclass {
    // Definition of subclass
}
```

#### extension

```swift
extension SomeType {
    // New functionality
}

extension SomeType: SomeProtocol, AnotherProtocol {
    // Implementation of protocol requirements
}

extension Double {
    var km: Double { return self * 1_000.0 }
    var m: Double { return self }
    var cm: Double { return self / 100.0 }
    var mm: Double { return self / 1_000.0 }
    var ft: Double { return self / 3.28084 }
}
```

#### protocol

```swift
protocol MyProtocol {
    var name: String { get }
    
    init(name:String)
}

struct FirstStruct: MyProtocol {
    var name: String
    init(name:String) {
        self.name = name
    }// You can omit these codes in structure because of its default initializer
}

struct SecondStruct {
    var name: String
}

extension SecondStruct: MyProtocol {
    //	Some Code
}

class ClassName: SuperClass, MyProtocol {
    // Defination of Class
    // Implementation of ProtocolName
}
```

#### Equatable, Comparable, Hashable, Identifiable, Codable

```swift
//  Equatable, Comparable, Hashable
struct Birthday: Equatable, Comparable, Hashable {
    let year: Int
    let month: Int
    let day: Int
    
    static func < (lhs: Birthday, rhs: Birthday) -> Bool {
        if lhs.year != rhs.year {
            return lhs.year < rhs.year
        } else if lhs.month != rhs.month {
            return lhs.month < rhs.month
        } else {
            return lhs.day < rhs.day
        }
    }
}

//  Identifiable, Codable
struct Person: Equatable, Identifiable, Codable {
    var name: String
    lazy var birthday = Birthday(year: 0, month: 0, day: 0)
    var id = UUID()
    
    
    static func ==(lhs: Person, rhs:Person) -> Bool {
        return lhs.name == rhs.name
    }
}

var personOne = Person(name: "Jobs")
personOne.birthday = Birthday(year: 1955, month: 2, day: 24)
var personTwo = Person(name: "Turing")
personTwo.birthday = Birthday(year: 1912, month: 6, day: 23)

if personOne == personTwo {
    print("They are the same person.")
} else {
    print("They are different.")
}

if personOne.birthday > personTwo.birthday {
    print("Jobs was younger than Turing.")
} else if personOne.birthday == personTwo.birthday {
    print("They were born in the same day.")
} else {
    print("Jobs was older than Turing.")
}

// Hashable
let birthdays = [personOne.birthday: personOne, personTwo.birthday: personTwo]
```



### URLSession 

```swift
URLSession.shared.dataTask(with: url) { (data, response, error) in }.resume()
```



