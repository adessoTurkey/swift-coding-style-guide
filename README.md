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
### Let’s take for example this code:

```
let isPositionCorrect = false
if isPositionCorrect {
    updateUI("Position Correct", isPositionCorrect)
} else {
    updateUI("Position InCorrect", isPositionCorrect)
}

```

If we look into this piece of code we see that the call to updateUI function is duplicated twice. Now this is a bad code because from maintainability perspective if the method definition has changed then you need to change it twice for example now the method takes 2 parameters what if we need to change it to take 3 parameters we have to change it in 2 places.

**To fix that we have to follow the DRY principle:**:

```
let message = isPositionCorrect ? "Position Correct" : "Position InCorrect"
updateUI(message, isPositionCorrect)
```

So in this case if we need to change the function we will change only one place, no duplication any more.

### Let's take for the other one example:

By creating an extension on ShowAlert protocol, all conforming types automatically gain showAlert() method implementation without any additional modification. 


```
protocol ShowingAlert {
    func showAlert(title: String, message: String)
}

extension ShowingAlert where Self: UIViewController {
    func showAlert(title: String, message: String) {
        let alertController = UIAlertController(title: title, message: message, preferredStyle: .alert)
        let dismissAction = UIAlertAction(title: "OK", style: .default, handler: nil)
        alertController.addAction(dismissAction)
        present(alertController, animated: true)
    }
}
```

All that’s left to do is make each view controller requiring error handling conform to ShowingAlert:

```
class LoginViewController: ShowingAlert { }
class HomeViewController: ShowingAlert { }
```

Now you can use showAlert in all and only those view controllers that conform to the protocol — you have full control over who can access your method. There’s also no code duplication: showAlert is implemented only once in a protocol extension. 

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
