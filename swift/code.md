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

#### protocal

```swift

```







