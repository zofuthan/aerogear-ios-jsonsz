# aerogear-ios-jsonsz [![Build Status](https://travis-ci.org/aerogear/aerogear-ios-jsonsz.png)](https://travis-ci.org/aerogear/aerogear-ios-jsonsz)

Serialize 'Swift' objects back-forth from their JSON representation the 'easy way'.

Here is a typical example usage:

```swift
class Contact : JSONSerializable {
    var first: String?  
    var last: String?   
    var addr: Address?

    required init() {}

    class func map(source: JsonSZ, object: Contact) {
        object.first <= source["first"]
        object.last <= source["last"]
        object.addr <= source["addr"]
    }
}

class Address: JSONSerializable {

    var street: String?
    var poBox: Int?
    var city: String?
    var country: String?

    var arr:[String]
    
    required init() {}
    
    class func map(source: JsonSZ, object: Address) {
        object.street <= source["street"]
        object.poBox <= source["poBox"]
        object.city <= source["city"]
        object.country <= source["country"]
    }
}

// construct object
let address =  Address()
address.street = "Street"
address.poBox = 100
address.city="New York"
address.country = "US"

let user = User()
user.first = "John"
user.last = "Doe"
// assign Address to User
user.addr = address

// initialize serializer
let serializer = JsonSZ()

// serialize ToJSON
let JSON = serializer.toJSON(user)
// ..send json to server

// serialize fromJSON
let user = serializer.fromJSON(JSON, to:User.self)

// user now should be initialized
println(user.first!)
...
```

As long as your model object implements the ```JSONSerializable``` protocol and its required methods of ```init``` and ```map```, the ```JsonSZ``` class should be able to serialize and deserialize your objects to JSON. The library supports all the primitive types including arrays and dictionaries plus relationship between the objects (as shown by the User, Address example above). Head over to our [unit tests](https://github.com/aerogear/aerogear-ios-jsonsz/blob/master/AeroGearJsonSZTests/AeroGearJsonSZTests.swift) for more examples usage.

Give it a go and let us know if it does help you on your projects!

Last, we would like to give appreciation and credit to the existing serialization libraries of [ObjectMapper](https://github.com/Hearst-DD/ObjectMapper) and [SwiftMapper](https://github.com/kam800/SwiftMapper) for giving us an initial bootstrap and ideas to base our development of this library. Thank you guys!

## Adding the library to your project 
To add the library in your project, you can either use [Cocoapods](http://cocoapods.org) or manual install in your project. See the respective sections below for instructions:

### Using [Cocoapods](http://cocoapods.org)
At this time, Cocoapods support for Swift frameworks is supported in a [pre-release](http://blog.cocoapods.org/Pod-Authors-Guide-to-CocoaPods-Frameworks/). In your ```Podfile``` add:

```
pod 'AeroGearJsonSZ'
```

and then:

```bash
pod install
```

to install your dependencies

### Manual Installation
Follow these steps to add the library in your Swift project:

1. Add AeroGearJsonSZ as a [submodule](http://git-scm.com/docs/git-submodule) in your project. Open a terminal and navigate to your project directory. Then enter:
```bash
git submodule add https://github.com/aerogear/aerogear-ios-jsonsz.git
```
2. Open the `aerogear-ios-jsonsz` folder, and drag the `AeroGearJsonSZ.xcodeproj` into the file navigator in Xcode.
3. In Xcode select your application target  and under the "Targets" heading section, ensure that the 'iOS  Deployment Target'  matches the application target of AeroGearJsonSZ.framework (Currently set to 8.0).
5. Select the  "Build Phases"  heading section,  expand the "Target Dependencies" group and add  `AeroGearJsonSZ.framework`.
7. Click on the `+` button at the top left of the panel and select "New Copy Files Phase". Rename this new phase to "Copy Frameworks", set the "Destination" to "Frameworks", and add `AeroGearJsonSZ.framework`.


If you run into any problems, please [file an issue](http://issues.jboss.org/browse/AEROGEAR) and/or ask our [user mailing list](https://lists.jboss.org/mailman/listinfo/aerogear-users). You can also join our [dev mailing list](https://lists.jboss.org/mailman/listinfo/aerogear-dev).  
