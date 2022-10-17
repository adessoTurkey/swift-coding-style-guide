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
* <a id='protocol-extension-dry'></a>(<a href='#protocol-extension-dry'>link</a>)
We can extract code snippets that do the same job into a single function.

**Preferred**
```swift
func sum(a: Int, b: Int) -> Int { return a + b }

func calculateTwoProperties() {
    let result = sum(a: firstValue, b: secondValue)
}
```

**Not Preffered**
```swift
func calculateTwoProperties() {
    let result = firstValue + secondValue
}
```

## Use Early Exit


## Write Shy Code


## Minimal Imports


## Protocol Conformance


## Function Declarations


## Memory Management


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
