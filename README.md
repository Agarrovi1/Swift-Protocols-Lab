
## Protocols Lab

## Instructions for lab submission 

1. Fork the assignment repo
1. Clone your Fork to your machine
1. Complete the lab
1. Push your changes to your Fork
1. Submit a Pull Request back to the assignment repo
1. Paste a link of the pull request on Canvas and submit

<pre> 
Question 1.
Create a Human class with two properties: name of type String, and age of type Int. You'll need to 
create a memberwise initializer for the class. Initialize two Human instances.

Make the Human class adopt the CustomStringConvertible. Print both of your previously initialized
Human objects.

Make the Human class adopt the Equatable protocol. Two instances of Human should be considered equal
if their names and ages are identical to one another. Print the result of a boolean expression 
evaluating whether or not your two previously initialized Human objects are equal to eachother
(using ==). Then print the result of a boolean expression evaluating whether or not your two
previously initialized Human objects are not equal to eachother (using !=).

Make the Human class adopt the Comparable protocol. Sorting should be based on age. Create another
three instances of a Human, then create an array called people of type [Human] with all of the
Human objects that you have initialized. Create a new array called sortedPeople of type [Human] 
that is the people array sorted by age.
</pre> 

</br> </br> 
```swift
class Human: CustomStringConvertible, Equatable, Comparable {
static func < (lhs: Human, rhs: Human) -> Bool {
return lhs.age < rhs.age
}

static func == (lhs: Human, rhs: Human) -> Bool {
return lhs.name == rhs.name && lhs.age == rhs.age
}
var description: String {
return "I am \(name) and i am \(age) years old"
}

var name: String
var age: Int

init(name: String, age: Int) {
self.name = name
self.age = age
}
}
//a
let crowley = Human(name: "Crowley", age: 30)
let azir = Human(name: "Aziraphael", age: 31)
//b
print(crowley)
print(azir)
//c
print(crowley == azir)
print(crowley != azir)
//d
let diana = Human(name: "Diana", age: 29)
let steve = Human(name: "Steve", age: 27)
let candy = Human(name: "Candy", age: 40)
let arr = [crowley,azir,diana,steve,candy]
let sortedPeople = arr.sorted()
print(sortedPeople)
```

<pre> 
Question 2. 
Create a protocol called Vehicle with two requirements: a nonsettable numberOfWheels property of
type Int, and a function called drive().

Define a Car struct that implements the Vehicle protocol. numberOfWheels should return a value of 4,
and drive() should print "Vroom, vroom!" Create an instance of Car, print its number of wheels, 
then call drive().

Define a Bike struct that implements the Vehicle protocol. numberOfWheels should return a value of 2,
and drive() should print "Begin pedaling!". Create an instance of Bike, print its number of wheels,
then call drive().
</pre>  
```swift
//a
protocol Vehicle {
var numberOfWheels: Int { get }
func drive()
}

//b
struct Car: Vehicle {
var numberOfWheels: Int = 4

func drive() {
print("Vroom, vroom!")
}
}
var lamborgini = Car()
print(lamborgini.numberOfWheels)
lamborgini.drive()

//c
struct Bike: Vehicle {
var numberOfWheels: Int = 2

func drive() {
print("Begin pedaling!")
}
}
var onoda = Bike()
print(onoda.numberOfWheels)
onoda.drive()
```

</br> </br> 

<pre> 
Question 3. 
// Given the below two protocols, create a struct for penguin(a flightless bird) and an eagle.
Give your structs some properties and have them conform to the appropriate protocols.

protocol Bird {
 var name: String { get }
 var canFly: Bool { get }
}

protocol Flyable {
 var airspeedVelocity: Double { get }
}
</pre> 
```swift
protocol Bird {
var name: String { get }
var canFly: Bool { get }
}

protocol Flyable {
var airspeedVelocity: Double { get }
}

struct Penguin: Bird {
var name: String
var canFly: Bool = false
}

struct Eagle: Bird, Flyable {
var name: String
var canFly: Bool = true

var airspeedVelocity: Double
}
```

</br> </br> 

<pre>
Question 4. 
// Create a protocol called Transformation

// create a mutating method called transform

// Make an enum called SuperHero (have it conform to Transformation) and an instance of it named
bruceBanner. Make it so that when the transform function is called that bruceBanner turns from 
.notHulk to .hulk.

enum SuperHero: Transformation {
    // write code here.
}

Example Output: 
var bruceBanner = SuperHero.notHulk

bruceBanner.transform() . // hulk

bruceBanner.transform()  // notHulk
</pre> 
```swift
protocol Transformation {
mutating func transform()
}

enum SuperHero: Transformation {
case notHulk
case hulk

mutating func transform() {
switch self {
case .notHulk:
self = .hulk
case .hulk:
self = .notHulk
}
}
}

var bruceBanner = SuperHero.notHulk
bruceBanner.transform()
bruceBanner.transform()
```
</br> </br> 

<pre>
Question 5. 
// 1. Create a protocol called Communication

// 2. Give it a property called talk, of type String, and assign it an explicit getter.

// 3. Create three Classes. Cow, Dog, Cat.

// 4. Have your three classes conform to Communication

// 5. talk should return a unique message for each animal when talk is called.

// 6. Put an instance of each of your Classes in an array.

// 7. Iterate over the array and have them print talk.
</pre> 
```swift
//a,b
protocol Communication {
var message: String { get }
}
//c,d,e
class Dog: Communication {
var message: String = "Bark"
}
class Cat: Communication {
var message: String = "Meow"
}
class Cow: Communication {
var message: String = "Moo"
}
//f
var dog = Dog()
var cat = Cat()
var cow = Cow()
let animals = [dog.message,cat.message,cow.message]
//g
for a in animals {
print(a)
}
```

</br> </br>
Question 6.
The HeartRateReceiver class below represents a very simplified example of a class dedicated to receiving information from fitness tracking hardware with monitoring heart rate. The function startHeartRateMonitoringExample will generate random heart rates and assign them to currentHR, simulating how an instance of HeartRateReceiver may pick up on new heart rate readings at specific intervals.

HeartRateViewController below is a view controller that will present the heart rate information to the user. Throughout the exercises below you'll use the delegate pattern to pass information from an instance of HeartRateReceiver to the view controller so that anytime new information is obtained it is presented to the user.

```swift
class HeartRateReceiver {
var currentHR: Int? {
didSet {
if let currentHR = currentHR {
print("The most recent heart rate reading is \(currentHR).")
} else {
print("Looks like we can't pick up a heart rate.")
}
}
}

func startHeartRateMonitoringExample() {
for _ in 1...10 {
let randomHR = 60 + Int.random(in: 0...15)
currentHR = randomHR
Thread.sleep(forTimeInterval: 2)
}
}
}

class HeartRateViewController: UIViewController {
var heartRateLabel: UILabel = UILabel()
}
```
First, create an instance of HeartRateReceiver and call startHeartRateMonitoringExample. Notice that every two seconds currentHR get set and prints the new heart rate reading to the console.

In a real app, printing to the console does not show information to the user. You need a way of passing information from the HeartRateReceiver to the HeartRateViewController. To do this, create a protocol called HeartRateReceiverDelegate that requires a method heartRateUpdated(to bpm:) where bpm is of type Int and represents the new rate as beats per minute. Since playgrounds read from top to bottom and the two previously declared classes will need to use this protocol, you'll need to declare this protocol above the declaration of HeartRateReceiver.

Now make HeartRateViewController adopt the protocol you've just created. Inside the body of the required method you should set the text of heartRateLabel and print "The user has been shown a heart rate of ."

Now add a property called delegate to HeartRateReceiver that is of type HeartRateReceiverDelegate?. In the didSet of currentHR where currentHR is successfully unwrapped, call heartRateUpdated(to bpm:) on the delegate property.

Finally, return to the line of code just after you initialized an instance of HeartRateReceiver. Initialize an instance of HeartRateViewController. Then, set the delegate property of your instance of HeartRateReceiver to be the instance of HeartRateViewController that you just created. Wait for your code to compile and observe what is printed to the console. Every time that currentHR gets set, you should see both a printout of the most recent heart rate, and the print statement stating that the heart rate was shown to the user.

```swift
protocol HeartRateRecieverDelegate {
func heartRateUpdated(toBPM: Int)
}

class HeartRateReceiver {
var delegate: HeartRateRecieverDelegate?
var currentHR: Int? {
didSet {
if let currentHR = currentHR {
print("The most recent heart rate reading is \(currentHR).")
self.delegate?.heartRateUpdated(toBPM: currentHR)
} else {
print("Looks like we can't pick up a heart rate.")
}
}
}

func startHeartRateMonitoringExample() {
for _ in 1...10 {
let randomHR = 60 + Int.random(in: 0...15)
currentHR = randomHR
Thread.sleep(forTimeInterval: 2)
}
}
}

class HeartRateViewController: UIViewController, HeartRateRecieverDelegate {
func heartRateUpdated(toBPM: Int) {
heartRateLabel.text = "\(toBPM) beats per minute"
print("The user has been shown a heart rate of \(toBPM)")
}

var heartRateLabel: UILabel = UILabel()
}

var sampleHeart = HeartRateReceiver()
//sampleHeart.startHeartRateMonitoringExample()
var sampleVC = HeartRateViewController()
sampleHeart.delegate = sampleVC
sampleHeart.startHeartRateMonitoringExample()
```
