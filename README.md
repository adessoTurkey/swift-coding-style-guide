Swift Coding Style Guide
============================

The coding standards adopted by adesso Turkey for the iOS platform.

Table of Contents
-----------------

- [DRY](#dry)
- [Use Early Exit](#use-early-exit)
- [Write Shy Code](#write-shy-code)
- [Minimal Imports](#minimal-imports)
- [Protocol Conformance](#protocol-conformance)
- [Function Declarations](#function-declarations)
- [Memory Management](#memory-management)
- [License](#license)

## DRY (Don't Repeat Yourself)


## Use Early Exit


## Write Shy Code


## Minimal Imports


## Protocol Conformance


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

## Memory Management

A memory leak must not be created in the source code. Retain cycles should be prevented by using either `weak` and `unowned` references. In addition, value types (e.g., `struct`, `enum`) can be used instead of reference types (e.g., `class`).

* <a id='optional-binding-over-memory-management'></a>(<a href='#optional-binding-over-memory-management'>link</a>)
Always use `[weak self]` or `[unowned self]` with `guard let self = self else { return }`.

**Preferred**
```swift
someMethod { [weak self] someResult in
  guard let self = self else { return }
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
  guard let self = self else { return }
  let result = self.updateResult(someResult)
  self.updateUI(with: result)
}
```

**Not Preferred**
```swift
// self may be deallocated inside closure
someMethod { [unowned self] someResult in
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
