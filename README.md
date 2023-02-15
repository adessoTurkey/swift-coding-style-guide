Swift Coding Style Guide
============================

The coding standards adopted by adesso Turkey for the iOS platform.

Table of Contents
-----------------

- [DRY](#dry)
- [Use Early Exit](#use-early-exit)
- [Write Shy Code](#write-shy-code)
- [Minimal Imports](#minimal-imports)
- [Protocol Declarations](#protocol-declarations)
- [Protocol Conformance](#protocol-conformance)
- [Function Declarations](#function-declarations)
- [Closure Expressions](#closure-expressions)
- [Memory Management](#memory-management)
- [If Let Shorthand](#if-let-shorthand)
- [License](#license)

## DRY (Don't Repeat Yourself)

The simple meaning of DRY is don’t write the same code repeatedly.

* <a id='duplicate-call-function-dry'></a>(<a href='#duplicate-call-function-dry'>link</a>)
Instead of preventing code repetition and calling the same function more than once, we should prefer the following method.

**Preferred**
```swift
let message = isPositionCorrect ? "Position Correct" : "Position InCorrect"
updateUI(message, isPositionCorrect)
```

**Not Preffered**
```swift
let isPositionCorrect = false
if isPositionCorrect {
    updateUI("Position Correct", isPositionCorrect)
} else {
    updateUI("Position InCorrect", isPositionCorrect)
}
```
* <a id='protocol-extension-dry'></a>(<a href='#protocol-extension-dry'>link</a>)
By creating an extension on ShowAlert protocol, all conforming types automatically gain showAlert() method implementation without any additional modification. 

**Preferred**
```swift
protocol ShowingAlert {
    func showAlert()
}

extension ShowingAlert where Self: UIViewController {
    func showAlert() {
        // ...
    }
}

class LoginViewController: ShowingAlert { }
class HomeViewController: ShowingAlert { }
```

**Not Preffered**
```swift
class LoginViewController {
    func showAlert() {
        // ...
    }
}

class HomeViewController: ShowingAlert { 
    func showAlert() {
        // ...
    }
}
```
* <a id='same-job-single-func-dry'></a>(<a href='#same-job-single-func-dry'>link</a>)
Extract code snippets with the same job into a single function.

**Preferred**
```swift
func sum(a: Int, b: Int) -> Int { return a + b }

func calculateTwoProperties() {
    let result = sum(a: firstValue, b: secondValue)
}
```

**Not Preffered**
```swift

let firstValue: Int = 5
let secondValue: Int = 12

func calculateTwoProperties() {
    let result = firstValue + secondValue
}
```

## Use Early Exit

* <a id='use-early-exit-with-guard'></a>(<a href='#use-early-exit-with-guard'>link</a>)
In functions that take parameters with early exit instead of wrapping the source code in an if loop statement, the condition that the loop is not executed should be added first, and if this is the case, it should return.

**Preferred**
```swift
func function(items: [Int]) {
    guard !items.isEmpty else { return }
    for item in items {
        // do something
    }
}
```

**Not Preffered**
```swift
func function(items: [Int]) {
    if items.count > 0 {
        for item in items {
            // do something
        }
    }
}
```

## Write Shy(Law Of Demeter) Code

* <a id='write-shy-code'></a>(<a href='#write-shy-code'>link</a>)
Write shy code that makes objects loosely coupled. Write everything with the smallest scope possible and only increase the scope if it really needs to.

**Preferred**
```swift
protocol PrefferedVMProtocol {
    func changeUserName(name: String)
}

struct User {
    var name: String?
}

class PrefferedVM: PrefferedVMProtocol {
    private var user: User
    
    init(user: User) {
        self.user = user
    }
    
    func changeUserName(name: String) {
        user.name = name
    }
}

let viewModel: PrefferedVMProtocol = PrefferedVM(user: User(name: "Test"))
viewModel.changeUserName(name: "Preffered")
```

**Not Preffered**
```swift
class NotPrefferedVM {
    var user: User
    
    init(user: User) {
        self.user = user
    }
}

let viewModel = NotPrefferedVM(user: User(name: "Test"))
viewModel.user.name = "Not Preffered"
```


## Minimal Imports

* <a id='minimal-imports'></a>(<a href='#minimal-imports'>link</a>)
Import only the modules a source file requires. 

**Preferred**
```swift
import UIKit
var textField: UITextField
var numbers: [Int]
```

**Not Preffered**
```swift
import UIKit
import Foundation
var textField: UITextField
var numbers: [Int]
```

**Preffered**
```swift
import Foundation
var numbers: [Int]
```

**Not Preffered**
```swift
import UIKit
var numbers: [Int]
```

## Protocol Declarations


## Protocol Conformance

When adding protocol conformance to a model, separate each into an extension and use // MARK: - comment.

* <a id='optional-binding-over-protocol-conformance'></a>(<a href='#optional-binding-over-protocol-conformance'>link</a>)

**Preferred**
```swift
class MyViewController: UIViewController {
  // class stuff
}

// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
  // table view data source
}

// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
  // scroll view delegate
}
```

**Not Preferred**
```swift
class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
  // all
}
```

## Function Declarations

* <a id='function-naming-long-declaration'></a>(<a href='#function-naming-long-declaration'>link</a>)
Keep function declarations short, if long, then use a line break after each parameter.

**Preferred**
```swift
func calculateCost(quantity: Int,
                   realPrice: Double,
                   discountRate: Double,
                   taxRate: Double,
                   serviceCharge: Double) -> Double {
    ...
}
```

**Not Preferred**
```swift
func calculateCost(quantity: Int, realPrice: Double, discountRate: Double, taxRate: Double, serviceCharge: Double) -> Double {
    ...
}
```

* <a id='function-with-long-declaration-invocation'></a>(<a href='#function-with-long-declaration-invocation'>link</a>)
Invoke functions with a long declaration by using a line break for each parameter.

**Preferred**
```swift
let result = calculateCost(quantity: 5,
                           realPrice: 100,
                           discountRate: 25,
                           taxRate: 10,
                           serviceCharge: 5)
```

**Not Preferred**
```swift
let result = calculateCost(quantity: 5, realPrice: 100, discountRate: 25, taxRate: 10, serviceCharge: 5)
```

**Not Preferred**
```swift
let result = calculateCost(
    quantity: 5,
    realPrice: 100,
    discountRate: 25,
    taxRate: 10,
    serviceCharge: 5)
```

* <a id='function-naming-assistive-words'></a>(<a href='#function-naming-assistive-words'>link</a>)
Use prepositions or assistive words in the parameter naming instead of function naming.

**Preferred**
```swift
func displayPopup(with message: String) {
    ...
}
```

**Not Preferred**
```swift
func displayPopupWith(message: String) {
    ...
}
```

* <a id='function-avoid-void-return'></a>(<a href='#function-avoid-void-return'>link</a>)
Avoid from `Void` return type.

**Preferred**
```swift
func someMethod() {
    ...
}
```

**Not Preferred**
```swift
func someMethod() -> Void {
    ...
}
```

## Closure Expressions

* <a id='closure-unused-parameter'></a>(<a href='#closure-unused-parameter'>link</a>)
Use an underscore (`_`) for the name of the unused closure parameter.

**Preferred**
```swift
// Only `data` parameter is used
someCompletion { data, _, _ in
    handle(data)
}
```

**Not Preferred**
```swift
// `error` and `succeeded` parameters are unused
someCompletion { data, error, succeeded in
    handle(data)
}
```

* <a id='trailing-closure-syntax'></a>(<a href='#trailing-closure-syntax'>link</a>)
Use trailing closure syntax when a function has only one closure parameter that is at the end of the argument list.

**Preferred**
```swift
someMethod(options: [.option1]) { result in
    print(result)
}
        
otherMethod(options: [.option1],
            action: { index in
            print(index)
},
            completion: { result in
    print(result)
})
```

**Not Preferred**
```swift
someMethod(options: [.option1], completion: { result in
    print(result)
})
        
otherMethod(options: [.option1], action: { index in
    print(index)
}) { result in
    print(result)
}
```

* <a id='closure-space-and-line-break-syntax'></a>(<a href='#closure-space-and-line-break-syntax'>link</a>)
Use space or line break inside and outside of the closure (if necessary) to increase readability.

**Preferred**
```swift
let activeIndices = items.filter { $0.isActive }.map { $0.index }

let activeIndices = items.filter({ $0.isActive }).map({ $0.index })

let activeIndices = items
    .filter { $0.isActive }
    .map { $0.index }

let activeIndices = items
    .filter {
        $0.isActive
    }
    .map {
        $0.index
    }
```

**Not Preferred**
```swift
let activeIndices = items.filter{$0.isActive}.map{$0.index}

let activeIndices = items.filter( { $0.isActive } ).map( { $0.index } )

let activeIndices = items
    .filter{$0.isActive}
    .map{$0.index}

let activeIndices = items
    .filter{
        $0.isActive
    }
    .map{
        $0.index
    }
```

* <a id='empty-parentheses-with-trailing-closure'></a>(<a href='#empty-parentheses-with-trailing-closure'>link</a>)
Don't use empty parentheses `()` when single parameter of a function is closure.

**Preferred**
```swift
func someClosure { result in
    ...
}
```

**Not Preferred**
```swift
func someClosure() { result in
    ...
}
```

* <a id='closure-avoid-void-return'></a>(<a href='#closure-avoid-void-return'>link</a>)
Avoid from `Void` return type.

**Preferred**
```swift
func someClosure { result in
    ...
}
```

**Not Preferred**
```swift
func someClosure { result -> Void in
    ...
}
```

## Memory Management

A memory leak must not be created in the source code. Retain cycles should be prevented by using either `weak` and `unowned` references. In addition, value types (e.g., `struct`, `enum`) can be used instead of reference types (e.g., `class`).

* <a id='optional-binding-over-memory-management'></a>(<a href='#optional-binding-over-memory-management'>link</a>)
Always use `[weak self]` or `[unowned self]` with `guard let self = self else { return }`.

**Preferred**
```swift
someMethod { [weak self] someResult in
  guard let self else { return } // Check out 'If Let Shorthand'
  let result = self.updateResult(someResult)
  self.updateUI(with: result)
}
```

**Not Preferred**
```swift
// Deallocation of self might occur between `let result = self?.updateResult(someResult)` and `self?.updateUI(with: result)`
someMethod { [weak self] someResult in
  let result = self?.updateResult(someResult)
  self?.updateUI(with: result)
}
```
* <a id='weak-over-unowned'></a>(<a href='#weak-over-unowned'>link</a>)
Use `[unowned self]` where the object can not be nil and 100% sure that object's lifetime is less than or equal to self. However, `[weak self]` should be preferred to `[unowned self]`.


**Preferred**
```swift
someMethod { [weak self] someResult in
  guard let self else { return } // Check out 'If Let Shorthand'
  let result = self.updateResult(someResult)
  self.updateUI(with: result)
}
```

**Not Preferred**
```swift
// self may be deallocated inside closure
someMethod { [unowned self] someResult in
  guard let self else { return } // Check out 'If Let Shorthand'
  let result = self.updateResult(someResult)
  self.updateUI(with: result)
}
```

## If Let Shorthand
Since (<a href='https://github.com/apple/swift-evolution/blob/main/proposals/0345-if-let-shorthand.md'>Swift 5.7</a>), we can simplfy the if-let & guard let blocks.

**Preferred**
```swift
if let value {
  print(value)
}
```

**Not Preferred**
```swift
if let value = value {
  print(value)
}
```

**Preferred**
```swift
someMethod { [weak self] someResult in
  guard let self else { return }
  let result = self.updateResult(someResult)
  self.updateUI(with: result)
}
```

**Not Preferred**
```swift
someMethod { [weak self] someResult in
  guard let self = self else { return }
  let result = self.updateResult(someResult)
  self.updateUI(with: result)
}
```
## License

```
Copyright 2020 adesso Turkey

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

[linkedin/jobs]: https://www.linkedin.com/company/adessoturkey/jobs/
